# Oportunidades: dónde F-Gestor-IA puede ser mejor que Sage

## A. Ya vas por delante (protégelo y véndelo)
1. **Todo en uno**: la cuenta auditada paga *Sage Active Starter* y la asesoría usa *Sage Despachos* para la contabilidad.
   F-Gestor-IA ya tiene asientos, cierres, reversión, mayor, sumas y saldos, balance y PyG. Es el argumento principal para dejar de pagar a Sage.
2. **IA documental más fiable**: evidencias por página, campos dudosos y nivel de confianza, revisión humana auditada y OCR local (privacidad).
   Sage se equivocó con una factura real con recargo de equivalencia (lo leyó como "IVA mínimo 5%" y descuadró la base del 10%).
3. **Integridad contable verificada** (inmutabilidad, cuadre, periodos bloqueados, pgTAP), mientras Sage Starter delega la contabilidad.
4. **Borradores de 303/130** que Starter no ofrece.
5. **Exportación completa** de 35 conjuntos de datos con manifiesto de originales.
6. **Bandeja de gestoría** con responsable y fecha límite dentro de la propia app (Sage manda las tareas a otro portal).

## B. Errores y debilidades de Sage observados (no los copies; corrígelos)
| Hallazgo en Sage | Cómo hacerlo mejor |
|---|---|
| La IA confunde el recargo de equivalencia con un tipo de IVA; la lista de impuestos de compras no ofrece las combinaciones con RE aunque existen en el maestro | Detectar RE (1,4 / 5,2 / 0,5 / 0,26 / 0,62 / 1 %), validar `base × tipo = cuota` y `Σ = total` por línea, y marcar el descuadre antes de contabilizar |
| "Programas, licencias y aplicaciones en la nube" va a 206 (inmovilizado) con régimen de gasto corriente | Distinguir licencia perpetua (206, amortizable) de suscripción SaaS (629) |
| "Cursos y talleres para empleados" va a 623 | 649 Otros gastos sociales |
| Categoría bancaria "Interés de deuda con institución de crédito" va a 662 "empresas del grupo" | 6623 Intereses de deudas con entidades de crédito |
| Diario por defecto de notas de abono = VEN, aunque existe REVEN | Usar REVEN y RECOM por defecto |
| Condición de pago por defecto "En efectivo" para clientes y proveedores | Pedirla en el onboarding (transferencia a 30 días es lo habitual en B2B) |
| Plantillas de e-mail con nombres internos en inglés y sin variables | Plantillas en español con variables `{cliente}`, `{número}`, `{total}`, `{vencimiento}` y `{enlace_pago}` |
| En los desplegables, Escape **selecciona** la opción resaltada | Escape cierra sin cambiar el valor |
| Filtros dependientes que se vacían solos (tipo de tercero → estado, tipo de factura → impuesto) | Conservar los filtros compatibles |
| Copilot Insights vacío ("No hay insights por ahora") | Insights deterministas que ya tienes (variación mensual, vencidas) más IA explicativa con cifras reales |
| Tareas, usuarios y suscripción en otro portal (app.sbc.sage.com) | Todo dentro de la misma app |
| VeriFactu sin configurar en la cuenta, con obligación desde el 01/01/2027 | Asistente obligatorio en el onboarding de cada empresa, con semáforo de cumplimiento en el panel |

## C. Matices de Sage que te faltan (backlog priorizado)

### P0 — legal o núcleo fiscal (antes de migrar clientes)
1. **Motor de impuestos en datos, no en código**: tabla de tipos (IVA, RE e IRPF) con fecha de vigencia, más una tabla de **regímenes fiscales**
   con código (C0031…C0045, C0076, C0107, C0122…), tipo (compras/ventas), cuentas de soportado y repercutido, e indicador de ISP.
   Cada línea de factura guarda tipo, régimen y cuenta. Con eso salen 303, 390 y los libros registro sin trabajo manual.
2. **Recargo de equivalencia** completo: indicador en el cliente, combinaciones IVA+RE, ventas C0044, compras con RE y columnas en el libro registro.
3. **Autorrepercusión** en intracomunitarias e ISP: un régimen con 472 y 477 genera los dos apuntes.
4. **Libro registro de facturas** emitidas y recibidas (IVA e IRPF), por ejercicio y rango de terceros, con RE, régimen, número de asiento,
   diario y origen; exportable a PDF y CSV.
5. **VERI\*FACTU conectado a `sales_invoices`**, con tres modos (VeriFactu / no VeriFactu por requerimiento / otro sistema), huella y
   "factura anterior registrada", comprobación de huellas y firmas, registro de eventos 01-10 y 90, descarga del XML y estado de presentación.
6. **Numeración al finalizar, no al crear el borrador**. Estructura de hasta 3 elementos (prefijo, número, ejercicio), separadores
   (guion, barra baja, barra, punto, espacio, ninguno), ceros a la izquierda con longitud, vista previa y "último número utilizado"
   para continuar la numeración de otro programa. Series propias para simplificadas y notas de abono.
7. **Factura simplificada** para particulares: sin NIF, cliente genérico, aviso de límite configurable (400 € por defecto).
8. **Revisión OCR con N líneas de IVA** y **categorías de compra** (las 17 de Sage, corregidas según el apartado B) → cuenta + régimen;
   categoría por defecto en el proveedor para que la IA la aplique sola.
9. **Recurrentes con ejecución automática** (cron o worker) y las frecuencias de Sage: diaria, semanal, mensual, anual, primer día, último día,
   último viernes y personalizada; fin nunca, en una fecha o tras N repeticiones; resumen en lenguaje natural.
10. **Reglas de conciliación bancaria**: 4 acciones, hasta 6 condiciones (contiene, intervalo ±días, intervalo ±€, campo de datos), contador
    de usos y las 10 reglas de serie; pestañas Por conciliar / Conciliados / Omitidos y revertir vinculación.

### P1 — paridad comercial
11. Condiciones de pago con plantillas, N plazos (% o importe restante, días desde emisión, forma de pago) y días de pago fijos del mes;
    condición por defecto para clientes y para proveedores.
12. Formas de pago con código UNECE (59, 10, 48, 20, 58) enlazadas a una cuenta de banco o de caja; caja 570 como tesorería.
13. Ficha de cliente completa: Empresa/Particular, CNAE, idioma del PDF, RE, cuentas 430/438, tarifa, grupo de descuento, % de descuento,
    bloqueos (facturas, albaranes, pedidos), notas finales legales por cliente, inactivo e importe vencido en la cabecera.
14. Proveedor editable y borrable, con categoría de compra, IRPF y régimen (1 General, 2 Nuevo inicio, 3 Arrendamiento).
15. Documento de venta: datos del cliente congelados y editables, mensaje en PDF frente a notas internas frente a notas finales,
    descuento global, panel de desglose y "Guardar y crear otra".
16. Envío real por e-mail con plantillas (8 tipos), copias, recordatorios de cobro y de presupuesto; adjunto PDF; registro del envío.
17. Diseñador PDF: logo (3 tamaños, 2 posiciones), datos de empresa y cliente a izquierda o derecha, fuente, paleta por tipo de documento
    (incluido recibo de cobro), fondo con opacidad, columnas de producto, pie de 2 líneas y vista previa en vivo.
    Extra que Sage ya tiene: importar el diseño desde un PDF con IA.
18. Tarifas que se aplican de verdad en los documentos (precio fijo, incremento %, importe) con tramos y fechas.
19. Informes de vencimientos y antigüedad de saldos (tramos configurables 30/45/60, rango de terceros, PDF).
20. Plan de cuentas en tabla con 5 niveles, naturaleza, tipo y mapeo a líneas de balance y PyG; cuentas por defecto configurables
    (incluidas ventas nacionales, UE y fuera de la UE).
21. Diarios separados (VEN, REVEN, COM, RECOM, BNC, CJ, GEN, APT, CIE).
22. Bandeja de compras por e-mail y aceptación de imágenes JPG/PNG.
23. Invitar usuarios desde la UI y pantalla de auditoría (ya tienes `audit_logs`).
24. Exportación de asientos para el asesor en formatos de terceros (A3, Contasol, Sage Despachos), útil mientras convives con otros despachos.

### P2 — pulido de experiencia
25. Listados con columnas configurables, filtros por columna con operadores, acciones en bloque y "Elementos: N".
26. Desplegables tipo tabla con "Gestionar lista" y "+ Crear" en línea.
27. Navegación anterior/siguiente respetando filtros y orden.
28. Comentarios internos por documento y "Información técnica" con IDs para soporte.
29. Smart Split de PDFs con varias facturas y app o PWA móvil para fotografiar tickets.
30. Presupuesto a un contacto potencial sin ficha de cliente.
31. Autocompletar CP, ciudad y provincia; departamentos de contactos; unidades de medida con decimales.
32. Cobro online con enlace "Pagar ahora" (Stripe o pago por banco).
33. API pública y webhooks.
34. Categorías de inmovilizado (21) con cuentas de activo, amortización acumulada, gasto y pérdidas, más cuadro de amortización.

## D. Ideas para superar a Sage (no las tiene)
- **Validación aritmética y fiscal en el OCR** antes de contabilizar (descuadres, tipo no vigente en la fecha, NIF inválido, RE sin cliente en RE).
- **Semáforo de cumplimiento por empresa** para el despacho: VeriFactu configurado, series correctas, modelos pendientes, facturas sin régimen.
- **Calendario fiscal** con 303, 130, 111, 115 y 349, y borradores precalculados.
- **Copilot con datos reales**: "¿qué proveedores han subido precio este trimestre?", "¿qué clientes pagan tarde?", respondido con consultas sobre tus tablas.
- **Portal del cliente** (ya tienes `fiscal_entity_members` viewer/uploader) para que el cliente suba tickets y vea su estado, sin pagar
  un segundo producto como Sage Active más Despachos.
