# Informes

Ruta: `/menu-page/reports` (página-menú con tarjetas agrupadas). Cada informe: botón ← volver, ✕, **Exportar a PDF** y
desplegable **Exportar** (se habilita al haber datos).

| Grupo | Informe | Ruta |
|---|---|---|
| Informes de terceros | Vencimientos | `/page/dead-line-payment` |
| | Antigüedad de saldos | `/page/aging-balance` |
| Cumplimiento normativo | Registro y presentación de facturas antifraude | `/page/sales-invoice-verifactu-register` |
| | Registro de eventos antifraude en presentación por requerimiento | `/page/sales-invoice-verifactu-events` |
| Otros informes | Libro registro de facturas | `/page/invoice-tax-summary` |
| Gestión de ficheros | Gestión de ficheros | `/list/file-management` |
| Exportaciones | Exportación para asesor fiscal | `/page/despachos-file-export` |
| | Exportación de todos los datos de la empresa | `/page/export-all-data-file` |

**No hay** informes contables (balance, PyG, sumas y saldos, mayor) ni modelos fiscales en este plan: la contabilidad la lleva la
asesoría en **Sage Despachos**, alimentada por la exportación de asientos.

## Vencimientos
- Filtros: Fecha de inicio · Fecha de fin · **Tipo de tercero** (Cliente / Proveedor) · Desde tercero · Hasta tercero (rango por código) ·
  **Estado** (Pendiente · Cobrado o pagado · Todos) · [Generar].
- Columnas: Fecha de vencimiento · Tercero · Número de factura · Importe · Importe cobrado o pagado · Importe pendiente · Forma de pago · Estado.
- Quirk: al cambiar el tipo de tercero se vacía el filtro Estado.

## Antigüedad de saldos
- Filtros: **Fecha de informe\*** · Tipo de tercero · Desde/Hasta tercero · **Primer plazo (30)** · **Segundo plazo (45)** · **Tercer plazo (60)** (editables).
- Columnas: Tercero · Total pendiente · Saldo no vencido · En primer plazo · En segundo plazo · En tercer plazo · Tras tercer plazo.
- Los enlaces del dashboard abren este informe con los tramos en la URL.

## Registro y presentación de facturas antifraude (VERI*FACTU / No VERI*FACTU)
- Botones: **Comprobar huellas** · ⋮ (**Resolver errores con soporte** · **Descargar XML de facturas**) · **Presentar facturas** (presentación por requerimiento).
- Filtros: Estado de presentación (Todas · Aceptadas · Pendientes) · Fecha de inicio\* · Fecha de fin\* (mes en curso por defecto) · [Generar] · Filtrar.
- Columnas: Número de factura · Fecha de factura · Cliente · Total · **Sistema de verificación de facturas** · **Estado de registro** ·
  Fecha de registro · **Factura anterior registrada** (encadenamiento) · Estado de presentación · Acciones.

## Registro de eventos antifraude (modo "presentación por requerimiento")
- Botones: **Comprobar huellas** · **Comprobar firmas** · ⋮.
- Texto: "Comparte los eventos del sistema de verificación con la AEAT cuando lo solicite. Solo se aplica al utilizar la presentación por requerimiento."
- Filtro **Tipo de evento** (lista oficial RD 1007/2023): 01 Inicio del funcionamiento como «NO VERI*FACTU» · 02 Fin del funcionamiento ·
  03 Lanzamiento de detección de anomalías en registros de facturación · 04 Detección de anomalías (integridad, inalterabilidad, trazabilidad) de
  registros de facturación · 05 Lanzamiento detección anomalías en registros de evento · 06 Detección de anomalías en registros de evento ·
  07 Restauración de copia de seguridad · 08 Exportación de registros de facturación de un periodo · 09 Exportación de registros de evento ·
  10 Registro resumen de eventos · 90 Otros eventos voluntarios.
- Columnas: Fecha de evento · Descripción · Número de factura · **Huella** · **Huella anterior** · **Firma electrónica** · Acciones.

## Libro registro de facturas
- Filtros: **Ejercicio\*** · Fecha inicio\* · Fecha fin\* · **Tipo de factura** (Emitida / Recibida) · **Tipo de impuesto** (IVA / IRPF) · Desde/Hasta tercero.
- Columnas: Fecha de asiento · Número de documento · Fecha de documento · Fecha de operación · Tercero · NIF · Importe total · Base imponible ·
  % impuesto · Cuota · **% recargo de equivalencia** · **Cuota de RE** · **Régimen fiscal** · Número de asiento · Diario · Origen.
- Quirk: cambiar Tipo de factura vacía Tipo de impuesto.

## Gestión de ficheros
- Repositorio documental de la empresa: drag&drop (máx. **20 MB**), columnas Nombre · Tamaño · Fecha de subida · Añadido por · Estado de subida ·
  Ver · **Comentarios** · Eliminar.

## Exportación para asesor fiscal
- "Genera un fichero de exportación con los asientos del periodo seleccionado." Fecha inicio/fin · [Generar].
- Historial: Fecha inicio · Fecha fin · **Generado por** (usuario de la asesoría) · Fecha de generación · Estado (Finalizada) · Acciones (Ver fichero · Eliminar).
- Botón **Integración con Sage Despachos** → modal con **Tenant ID** y **Business ID** + "Copiar detalles" para vincular la empresa en el software del despacho.

## Exportación de todos los datos de la empresa
- Empresa seleccionada (se cambia desde la barra superior) · [Generar] · tarjeta "Última exportación" con **Ver informe de errores** y **Descargar**.
