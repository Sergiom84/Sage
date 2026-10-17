# Inventario funcional de F-Gestor-IA (GFiscal)

Fuente: lectura read-only del repo clonado en `/Users/sergio/Desktop/Aplicaciones/GFiscal`
(github.com/Sergiom84/F-Gestor-IA) el 2026-10-16. Rutas relativas a ese repo.

## Resumen
Núcleo sólido: Ventas (presupuesto→pedido→albarán→factura, recurrentes, rectificativas totales), contabilización
de facturas, asientos con integridad (cuadre, inmutabilidad, reversión, cierres), cobros/pagos con conciliación CSV 1:1,
informes contables internos (PyG, balance, sumas y saldos, mayor), pipeline documental OCR+IA con revisión humana,
importación/exportación CSV/JSON.
Débil: fiscalidad (303/130 solo borrador interno; sin 111/115/180/190/347/349/390), VERI*FACTU desconectado de
`sales_invoices`, sin SII/TicketBAI/Facturae/SEPA/nóminas, IVA contabilizado en una sola cuenta (sin desglose por tipo),
sin recargo de equivalencia ni intracomunitarias/ISP, sin plan contable en tabla.
Las 9 migraciones de septiembre solo están probadas en BD local (`docs/20-implementation-results.md:3`).

## 1. Stack
- Next.js 16 App Router + React 19 + TS + Zod 4. Una sola página `/dashboard` con `?module=`/`?tab=`
  (`app/dashboard/page.tsx`, `app/dashboard/_sections/section-registry.tsx`).
- Ya existe un mapa de referencia de Sage Active en el repo: `docs/16-mapa-referencia-sage-active.md`,
  `src/lib/product/sage-active-reference.ts`.
- Supabase Auth email+password; signup público activo (contradice `scripts/invite-user.mjs`). Invitaciones solo por CLI.
- Supabase Postgres con RLS + `app_private` helpers; `pgmq` cola `document_processing`; bucket privado `document-files` (50 MB, pdf/png/jpeg).
- Multiempresa: `organizations` (despacho) → `fiscal_entities` (empresas). Empresa activa en cookie `gfiscal-company-{org}`.
  Clientes/proveedores/productos/empleados/tarifas a nivel organización (compartidos entre empresas).
- Server actions (`commercial-actions.ts` ~2.500 líneas, `accounting-actions.ts`, `actions.ts`); revisión OCR usa conexión
  Postgres directa sin RLS (`app/dashboard/actions.ts:237`).
- Worker documental (`src/workers/document-worker/`, `Dockerfile.worker`): pdfjs texto embebido → tesseract.js local (spa) →
  OpenAI Responses API con JSON Schema (`gpt-5.4-mini`), presupuesto IA mensual por org, duplicados sha256, reintentos.
- PDF con pdf-lib + borrador `.eml`. Integraciones externas: solo OpenAI (opcional).
- Render (producción), GitHub Actions (typecheck/test/build, pgTAP), ~130 tests unitarios, 7 pgTAP, e2e Playwright.

## 2. Pantallas
| Ruta | Qué hace |
|---|---|
| `/login` (`signup`, `recovery`) | Acceso/alta/recuperación |
| `/onboarding` | Alta de despacho (RPC `create_onboarding_workspace`) |
| `module=dashboard&tab=accounting` | KPIs PyG desde asientos |
| `tab=management` (Gestoría) | Bandeja gestoría, checks, panel documental |
| `tab=sales` (Ventas y compras) | Pendiente cobro/pago, vencidas, presupuestos pendientes |
| `module=sales&salesSection=quotes|orders|delivery-notes|invoices|recurring-invoices` | Ventas (`sales-workspace.tsx` 4.733 líneas) |
| `module=quotes` | Generador independiente de presupuestos/facturas + diseñador de plantillas |
| `module=purchases` | Compras: PDF, alta manual, Por revisar/Por pagar/Pagadas |
| `module=contacts` | Clientes, proveedores, empleados |
| `module=products` | Productos/servicios, tarifas, grupos de descuento |
| `module=banks` | Cuentas, CSV, contabilización, cobros/pagos, conciliación |
| `module=accounting` | Asientos, marcaje, cierres, inmovilizado |
| `module=tax` | Borradores 303 y 130 |
| `module=reports` | PyG, balance, sumas y saldos, mayor (CSV) |
| `module=settings` | Despacho, empresas, miembros, series, import/export |
| `/dashboard/review/[taskId]` | Revisión humana de extracción IA |
| `GET /api/data-export` | 35 datasets CSV/JSON |
| `GET /api/sales/[id]/export?format=pdf|eml` | PDF / .eml de factura |

## 3. Módulos (resumen)
- **Empresas:** `save_fiscal_company` valida NIF/CIF/NIE por dígito de control, CP 5 dígitos, sin NIF duplicado; solo owner/admin.
- **Roles:** owner/admin/accountant/reviewer/client + `fiscal_entity_members` viewer/uploader (portal cliente sin UI). Sin invitar desde UI.
- **Clientes:** campos completos (tipo, NIF, NIF-IVA, domicilio, IRPF por defecto…), direcciones múltiples, borrado lógico protegido.
  Contactos adicionales / condiciones de pago / condiciones de venta = "Próximamente" (`contacts-workspace.tsx:799-845,1066-1120`).
- **Proveedores:** alta + alta implícita al registrar compra; **sin edición ni borrado**.
- **Empleados:** solo alta.
- **Productos:** CRUD, duplicar, activar. Tarifas y grupos de descuento solo cabecera (sin líneas, no se aplican en ventas). Sin stock.
- **Ventas:** cabecera+líneas para 5 tipos; estados draft/open/booked/sent/accepted/rejected/overdue/paid/cancelled; totales en servidor;
  reglas IVA/IRPF por tipo de documento; conversión a factura sin doble facturación; PDF/.eml; envío solo `mailto:`/wa.me.
  Facturas inmutables tras emitir; "pagada" solo vía cobro. Rectificativas: serie `R-AAAA-XXXX`, total en negativo, sin R1-R5,
  sin contabilizar negativas. Recurrentes: generación idempotente de borradores, sin scheduler.
- **Series:** `PREFIJO-AAAA-0001` por empresa y tipo; número asignado al crear borrador → **riesgo de huecos**.
- **Compras:** alta manual (IVA 0/4/10/21, 1-250 líneas, sin duplicado nº+proveedor); desde OCR por trigger (sin proveedor vinculado ni retención).
  Panel de detalle con campos editables que no guardan; filtros sin acción. Sin categorías de gasto/tickets/deducibilidad/prorrata.
- **Documental IA:** el módulo más maduro (evidencias por página, campos dudosos, confianza). Revisión limitada a **un tipo de IVA y una línea**.
  Solo PDF (aunque el bucket admite imágenes). Entrada por email declarada pero no implementada.
- **Impuestos:** IVA por línea; IRPF; suplidos (440). Sin RE, intracomunitarias, ISP, prorrata, criterio de caja, REBU, OSS, exentos con causa.
- **Contabilidad:** diario GEN, asientos con cuadre, inmutables, reversión, cierres mensual/anual, bloqueo de periodo.
  `book_commercial_invoice`: 430/7xx/477/473/440 y 6xx/400/472/4751, una sola cuenta de gasto/ingreso por factura.
  Sin plan contable en tabla, sin regularización/cierre/apertura automáticos, sin analítica, sin libros oficiales.
- **Bancos:** IBAN mod-97, cuenta 57x, CSV `fecha;importe;concepto;referencia` (500 KB / 5.000 filas), cobros/pagos parciales,
  conciliación 1:1 exacta. Sin PSD2/Norma 43/reglas/1:N/previsión/remesas.
- **SEPA, nóminas, 111/115/180/190/347/349/390, SII/TicketBAI/Facturae:** no existen.
- **VERI*FACTU:** ledger interno encadenado por hash, solo CLI, ligado a `invoices` (OCR) y no a `sales_invoices`.
- **Inmovilizado:** alta/baja; sin cálculo ni cuadro de amortización.
- **Informes:** PyG, balance interno, sumas y saldos, mayor (CSV). Sin informes comerciales, aging detallado ni libros de IVA.
- **Import/Export:** CSV clientes/proveedores/productos/asientos (1-500 filas, idempotente); export 35 datasets.
- **Notificaciones:** no hay correo saliente ni recordatorios. **Auditoría:** `audit_logs` en 10 tablas, sin pantalla.

## 4. Madurez
| Módulo | Estado |
|---|---|
| Auth/onboarding/multiempresa | Completo básico |
| Usuarios y roles | Parcial |
| Clientes | Parcial-alto |
| Proveedores | Parcial (sin editar/borrar) |
| Empleados | Esqueleto |
| Productos | Completo básico |
| Tarifas/descuentos | Esqueleto |
| Presupuestos/pedidos/albaranes | Parcial-alto |
| Facturas emitidas | Completo (EUR estándar) |
| Rectificativas | Parcial |
| Recurrentes | Parcial (sin scheduler) |
| Series | Completo con riesgo de huecos |
| Compras manuales | Parcial |
| Documental OCR/IA | Completo MVP (1 tipo IVA en revisión) |
| Impuestos | Parcial |
| Asientos/cierres | Completo núcleo |
| Plan contable/regularización | TODO |
| Informes contables | Completo interno |
| Bancos/conciliación | Parcial (CSV, 1:1) |
| SEPA | TODO |
| 303/130 | Borrador interno |
| Resto de modelos | TODO |
| VERI*FACTU | Esqueleto |
| SII/TicketBAI/Facturae | TODO |
| Inmovilizado | Esqueleto |
| Nóminas | TODO |
| Notificaciones/correo | TODO |
| Auditoría | Parcial (sin UI) |

## 5. Riesgos a vigilar
- Huecos de numeración por asignar número al borrador.
- Acciones sin comprobación de rol/estado (solo RLS): `softDeleteSalesDocument`, `postAccountingEntry`, `markAccountingLines`,
  `close/lockClosingPeriod`, `writeOffFixedAsset`.
- Maestros compartidos entre empresas de una gestoría.
- Revisión OCR con conexión que salta RLS.
- VERI*FACTU no conectado a facturas emitidas.
- Signup público activo.
- IVA en una sola cuenta → sin casillas 303 ni libros registro.
