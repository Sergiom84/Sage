# Matriz comparativa — Sage Active (observado) vs F-Gestor-IA (repo GFiscal)

Leyenda: ✅ paridad · 🟡 parcial · ❌ falta en F-Gestor-IA · ⭐ F-Gestor-IA va por delante · P0/P1/P2 = prioridad sugerida.
Fuentes: fichas `modulos/*.md` (Sage) y `80_inventario_F-Gestor-IA.md` (tu app). Se han verificado con `grep` en el repo los huecos
de recargo de equivalencia, códigos de régimen fiscal, días de pago, categorías de compra, plantillas de e-mail y reglas bancarias.

> Contexto: la cuenta auditada es **Sage Active Starter** (sin contabilidad en menú). La contabilidad la hace la asesoría en **Sage Despachos**.
> Para vuestro caso (gestoría) hay que comparar contra **Starter + Despachos**: Sage cobra dos productos por lo que F-Gestor-IA puede dar en uno.

## 1. Plataforma y experiencia de uso
| Área | Sage Active | F-Gestor-IA | Estado | Prio |
|---|---|---|---|---|
| Multiempresa de despacho | Selector de empresa + lista de empresas cliente | `organizations → fiscal_entities`, cookie de empresa | ✅ | — |
| Roles | 4 fijos (Administrador, Contable, Admin. ventas y compras, Solo lectura) + permisos por área | owner/admin/accountant/reviewer/client | 🟡 | P2 |
| Invitar usuarios desde la UI | Sí (Añadir, Invitaciones pendientes) | Solo script CLI | ❌ | P1 |
| Registro de actividad (auditoría) | Pantalla con usuario, valor original/nuevo, filtros | `audit_logs` en BD sin pantalla | 🟡 | P2 |
| Tareas | Lista/kanban, prioridad, vencimiento, asignación (en portal aparte) | Bandeja de gestoría con responsable y fecha límite | 🟡 | P2 |
| Listados configurables | Columnas mostrar/ocultar/reordenar, altura de fila, filtros por columna con operadores, acciones en bloque | Búsqueda + estado + cliente, paginación servidor | 🟡 | P1 |
| Lookup con "Gestionar lista" y "+ Crear" | En todos los desplegables | No | ❌ | P1 |
| Navegación anterior/siguiente en detalle | Sí, respeta filtros | No | ❌ | P2 |
| Comentarios internos por documento | Sí (panel) | No (solo notas) | ❌ | P2 |
| "Información técnica" para soporte | IDs copiables | No | ❌ | P2 |
| Modal "Cambios sin guardar" | Sí | — | 🟡 | P2 |
| App móvil | iOS/Android (captura de tickets) | No (web) | ❌ | P2 |
| Copilot / IA conversacional | Chat de ayuda, "Redactar con Copilot", Insights (vacíos en esta cuenta) | IA solo en extracción documental | 🟡 | P2 |
| Onboarding guiado | Checklist "Configura tus productos" % | `/onboarding` de alta | 🟡 | P2 |

## 2. Ventas
| Área | Sage Active | F-Gestor-IA | Estado | Prio |
|---|---|---|---|---|
| Presupuesto/pedido/albarán/factura | Sí | Sí | ✅ | — |
| Presupuesto a contacto potencial (sin ficha) | Sí (nombre, e-mail, teléfono, país) | No (cliente obligatorio) | ❌ | P2 |
| Borrador → **Finalizar** con confirmación | Sí | Estados draft/open/booked… | 🟡 | P0 |
| Número asignado al finalizar | Sí (borrador sin número definitivo) | Asignado al crear borrador → huecos | ❌ | **P0** |
| Factura simplificada para particulares | Sí, por defecto, aviso > 400 € | No | ❌ | **P0** |
| Rectificativa / nota de abono | Serie compartida "facturas y notas de abono", diario de abono | Total en negativo, sin R1-R5, sin contabilizar | 🟡 | P0 |
| Datos del cliente congelados y editables en el documento | Pestaña "Información de cliente" | Snapshot de plantilla; cliente fijo | 🟡 | P1 |
| Idioma del PDF por cliente | Sí | No | ❌ | P2 |
| Mensaje en PDF / notas internas / notas finales legales | Tres campos separados + notas finales por cliente | Notas | 🟡 | P1 |
| Descuento por línea + descuento global % cliente | Sí, con totalizador de descuentos | % por línea | 🟡 | P1 |
| Panel de desglose de impuestos | Sí | Totales | 🟡 | P2 |
| Condiciones de pago con N plazos y días fijos | Sí | No (tablas sin uso) | ❌ | P1 |
| "Guardar y crear otra" | Sí | No | ❌ | P2 |
| Recurrentes: frecuencias | 8 (incl. último viernes, personalizada) + fin nunca/fecha/nº | semanal/mensual/trimestral/anual | 🟡 | P1 |
| Recurrentes: ejecución automática | Sí | Sin scheduler | ❌ | **P0** |
| Envío por e-mail con plantilla | 8 plantillas, CC, recordatorios | `mailto:`, wa.me, `.eml` | ❌ | P1 |
| Recordatorios de cobro / presupuesto | "Preparar recordatorios" | No | ❌ | P1 |
| Cobro online ("Pagar ahora") | Sí (comisión por transacción) | No | ❌ | P2 |
| Diseñador de plantilla PDF | Logo, posiciones, fuentes, paleta por tipo, fondo, pie, vista previa en vivo, Copilot desde PDF | Diseñador en módulo Presupuestos | 🟡 | P1 |
| IRPF en ventas | Propiedad del emisor (régimen General / Nuevo inicio / Arrendamiento) | Por línea con % por defecto del cliente | 🟡 | P1 |
| Bloquear facturas/albaranes/pedidos por cliente o producto | Sí | No | ❌ | P2 |

## 3. Compras y gestión documental
| Área | Sage Active | F-Gestor-IA | Estado | Prio |
|---|---|---|---|---|
| OCR/IA de facturas | Sí | Sí, con evidencias por página y confianza | ⭐ | — |
| Revisión con varios tipos de IVA | Rejilla con N líneas de IVA | Un solo tipo y una línea | ❌ | **P0** |
| Recargo de equivalencia en compras | Existe en maestro, **mal detectado** por su IA | No existe | ❌ | **P0** |
| Tipos 2 % / 5 % / 7,5 % | Sí | La IA los acepta; el alta manual solo 0/4/10/21 | 🟡 | P1 |
| Categoría de compra → cuenta + régimen | 17 categorías de negocio | No (solo en catálogo de referencia) | ❌ | **P0** |
| Categoría por defecto en el proveedor | Sí | No | ❌ | P0 |
| Detalle contable por línea (IVA, régimen, cuenta) | Sí | Una cuenta de gasto por factura | 🟡 | P0 |
| Vista partida documento/formulario + visor PDF | Sí (zoom, rotar, anotar) | Revisión con PDF por URL firmada | 🟡 | P2 |
| Bandeja por e-mail | `<alias>-facturascompra@…` | Declarada, no implementada | ❌ | P1 |
| Fotos JPG/PNG | Sí | Solo PDF (aunque el bucket admite imágenes) | ❌ | P1 |
| Smart Split (PDF con varias facturas) | Sí | No | ❌ | P2 |
| Estados de compra | 8 (Subiendo, Error de fichero, Pendiente, Por pagar, Parcial…, Vencida, Pagada) | Por revisar / Por pagar / Pagadas | 🟡 | P2 |
| Registrar pago con vencimientos parciales y descripción del asiento | Sí | Cobros/pagos parciales en Bancos | ✅ | — |
| Proveedor: editar / borrar | Sí | No | ❌ | P1 |
| IRPF por proveedor con régimen (1/2/3) | Sí | Importe de cabecera | 🟡 | P1 |

## 4. Fiscalidad y cumplimiento
| Área | Sage Active | F-Gestor-IA | Estado | Prio |
|---|---|---|---|---|
| Tipos impositivos con fecha de vigencia y % RE | 18 tipos | Constantes en código | ❌ | **P0** |
| Régimen fiscal / código de impuesto por línea (C00xx) | Sí → base para 303/390/libros | No | ❌ | **P0** |
| Autorrepercusión intracomunitaria / ISP | 472+477 automáticos | No | ❌ | P0 |
| Importaciones, bienes de inversión, créditos incobrables | Regímenes propios | No | ❌ | P1 |
| Libro registro de facturas emitidas/recibidas (IVA/IRPF) | Sí, con RE, régimen y nº de asiento | No | ❌ | **P0** |
| VERI\*FACTU (tiempo real / por requerimiento / otro) | Configurable, aviso 01/01/2027 | Ledger interno por CLI, no ligado a ventas | ❌ | **P0** |
| Huellas encadenadas, comprobar huellas/firmas, XML | Sí | Hash encadenado interno | 🟡 | P0 |
| Registro de eventos NO VERI\*FACTU (01-10, 90) | Sí | No | ❌ | P0 |
| Formas de pago con código UNECE (e-factura) | Sí | No | ❌ | P1 |
| Tipo de cliente Empresa/Particular (e-factura) | Obligatorio con aviso | `client_kind` | ✅ | — |
| Modelos 303/130 | No en Starter (los hace la asesoría) | Borrador interno | ⭐ | — |
| 111/115/347/349/390 | No en Starter | No | — | P1 |

## 5. Contabilidad
| Área | Sage Active (Starter + configuración) | F-Gestor-IA | Estado | Prio |
|---|---|---|---|---|
| Plan de cuentas en tabla (1.427 cuentas, 5 niveles, naturaleza, mapeo a informes) | Sí | Cuentas como texto libre | ❌ | **P0** |
| Longitud de cuenta 9 ampliable | Sí | 3-12 dígitos libres | 🟡 | P1 |
| Cuentas por defecto (430/438/400/700 nac./UE/extra/472/477/572/570) | Sí | Fijas en función SQL | 🟡 | P1 |
| Diarios (APT, BNC, CIE, CJ, COM, GEN, RECOM, REVEN, VEN) | Sí | Solo GEN | ❌ | P1 |
| Ejercicios con estado | Sí | Periodos de cierre mensual/anual | ✅ | — |
| Asientos, cierres, reversión, mayor, balance, PyG | No en Starter | Sí | ⭐ | — |
| Categorías de inmovilizado (21) con 4 cuentas por defecto | Sí | Alta/baja sin categorías | 🟡 | P2 |
| Exportación de asientos para el asesor | Sí (Sage Despachos) | Exportación genérica de 35 datasets | 🟡 | P1 |

## 6. Bancos y tesorería
| Área | Sage Active | F-Gestor-IA | Estado | Prio |
|---|---|---|---|---|
| Conexión bancaria (open banking) | Botón Conectar y Sincronizar todo | CSV | ❌ | P1 |
| Reglas de conciliación (4 acciones, 6 condiciones, tolerancias ±días/±€, contador de uso) | 10 de serie | No | ❌ | **P0** |
| Propuestas / Conciliados / Omitidos / revertir | Sí | Conciliación 1:1 exacta | 🟡 | P0 |
| Categorías bancarias + de ajuste (cambio, descuadres) | Sí | No | ❌ | P1 |
| Caja (efectivo) como cuenta de tesorería | Sí (570) | Solo cuentas bancarias | ❌ | P1 |
| IBAN → banco automático | Sí | Validación mod-97 | 🟡 | P2 |

## 7. Maestros, informes e importación
| Área | Sage Active | F-Gestor-IA | Estado | Prio |
|---|---|---|---|---|
| Cliente: pestañas Contactos / Condiciones de pago / Direcciones / Condiciones de venta | Operativas | Pestañas "Próximamente" | 🟡 | P1 |
| Cliente: CNAE, RE, idioma, cuenta y anticipos, notas finales, inactivo, importe vencido | Sí | Parcial | 🟡 | P1 |
| Autocompletar CP / ciudad / provincia | Sí | No | ❌ | P2 |
| Departamentos de contactos | 8 | No | ❌ | P2 |
| Tarifas (precio fijo / incremento % / importe) con tramos | Sí | Solo cabecera | 🟡 | P1 |
| Unidades de medida con decimales y categoría | 18 | 5 fijas | 🟡 | P2 |
| Vencimientos (rango de terceros, estado) y antigüedad (tramos 30/45/60) | Sí + PDF | Pendiente y vencidas en dashboard | 🟡 | P1 |
| Importación con historial (líneas importadas/pendientes, ver CSV, eliminar) y creación de cuentas que falten | Sí | Importación por lotes sin historial | 🟡 | P2 |
| Exportación completa de datos | Sí (1 botón) | 35 datasets CSV/JSON + manifiesto de originales | ⭐ | — |
| Gestión de ficheros (20 MB, comentarios) | Sí | Documental ligado a facturas | 🟡 | P2 |
| API pública + Marketplace | Sí | No | ❌ | P2 |
