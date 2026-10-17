# Ventas

Submenú: Presupuestos · Pedidos · Albaranes · Facturas · Facturas recurrentes.
En esta cuenta los listados de ventas están vacíos (el negocio solo registra compras), así que el detalle de un documento
emitido (acciones post-emisión, PDF, envío, rectificar) no se ha podido observar. Ver "Pendiente de observar" al final.

| Documento | Listado | Formulario |
|---|---|---|
| Presupuesto | `/list/sales-offer` | `/page/sales-offer` |
| Pedido | `/list/sales-order` | `/page/sales-order` |
| Albarán | `/list/sales-delivery-note` | `/page/sales-delivery-note` |
| Factura | `/list/sales-invoice` | `/page/sales-invoice` |
| Recurrente | `/list/sales-invoice-template` | panel "Programación" + plantilla |

## Listados (patrón común)
- Cabecera: título + Copilot Insights + desplegable **Configuración** (atajos a: Ventas y compras · Preferencias de documentos ·
  Productos y servicios · Plantillas de e-mail).
- Botones: **Crear** · **Acciones en bloque** (activa modo selección: "Seleccionar todo", "Elementos seleccionados: N",
  "Eliminar … seleccionadas") · buscador · Filtrar · Personalizar.
- Columnas por defecto: Estado · Fecha · Número · Referencia · Código de cliente · Cliente · Total · Base imponible · Editar · Eliminar.
- **Facturas — filtros extra arriba:** Inicio/Fin de fecha de creación + **Origen de factura** (multiselección):
  Creación manual · Importación · Factura recurrente.
- **Facturas — columnas opcionales:** Importe pendiente · Tipo · Fecha de vencimiento · Fecha de creación · Fecha de operación ·
  Provincia · % descuento a cliente · Descuento total a cliente · Número de identificación · Total IVA · Recargo de equivalencia.
- **Recurrentes — columnas:** Cliente · Número de identificación · NIF-IVA · Frecuencia · Fecha de inicio · Fecha de fin ·
  Repeticiones · Editar · Acciones. Texto: "Lleva un seguimiento de las facturas recurrentes y gestiónalas para tus clientes."

## Formulario de factura de venta
- Título "Factura de venta" + chip **Borrador** (el documento nace como borrador). Botón ✕ arriba a la derecha.
- **Cabecera:** Cliente\* (lookup multi-columna: Razón social · Nombre comercial · Número de identificación; Gestionar lista / + Crear)
  → al elegir muestra **Dirección de facturación**. Prefijo de documento (serie; "N/A" si no hay series) · Referencia ·
  Fecha de factura\* (hoy) · Fecha de operación.
- Al añadir la primera línea **el cliente queda bloqueado** (gris).
- **Pestañas:**
  1. *Productos y servicios* — rejilla editable: Producto o servicio (lookup) · Descripción · Cantidad · Precio unitario ·
     Descuento · Base imponible · (en pedidos/albaranes también **% IVA**) · Eliminar (🗑) · Acciones (⋮ → **Ver detalles contables**).
     Botón + Añadir.
  2. *Notas* — **Mensaje personalizado** (sale en el PDF, contador "Quedan 500 caracteres") · **Notas** internas ("No se muestran al
     cliente") · **Notas finales** (texto legal/cumplimiento normativo al pie, botón Editar, gestionado en configuración).
  3. *Información de cliente* — copia editable de los datos del cliente **en ese documento**: Código de cliente · Razón social\* ·
     País\* · Tipo de identificación\* · Número de identificación\* · NIF-IVA · **Idioma** (traduce títulos y cabeceras del PDF) ·
     Tarifa (código/nombre) · Grupo de descuentos (código/nombre) · **Recargo de equivalencia** · Tipo de e-mail · E-mail de factura ·
     Dirección de entrega / Dirección de facturación / Información de contacto (cada una con **Editar** y **Cambiar**).
- **Condiciones de pago** (bloque bajo las líneas): "Plazo 1 — Importe restante vence 0 días después de la fecha de la factura" +
  **Editar** → panel *Editar condiciones de pago*:
  - Condiciones de pago (plantillas): 50% ahora y 50% en 30 días · En efectivo · Pago a 30 días · Pago a fin de mes (+ Gestionar/Crear).
  - **Días de pago** (multiselección): "Último día del mes", 30…1 → vencimientos en días fijos del mes.
  - **Programación de pagos**: N plazos, cada uno con Tipo\* (Importe restante / …) · Valor · Días desde emisión de factura\* ·
    Forma de pago · 🗑. Botón **+ Añadir otro plazo**.
- **Totales de descuentos:** Sin descuento de producto · Descuento de producto · Sin descuento a cliente · **+ Añadir descuento a cliente**
  (campo "% descuento a cliente" global).
- **Totales y desglose de impuestos:** Total base imponible · Total IVA · Desglose de impuestos [**Ver**] (panel por tipo:
  Impuesto · Base imponible · Tipo de IVA · Cuota) · Total.
- **Barra inferior fija:** Total base imponible · Total IVA · Total · Cancelar · **Crear** (split → **Guardar y crear otra**).
- Validación en panel: "Campo obligatorio" en rojo. Modal "Cambios sin guardar" al salir.
- Quirk: en los combos, **Escape selecciona la opción resaltada** en vez de cerrar (fuente de errores).

### Detalles contables de línea (venta)
Panel con: Producto o servicio · **Tipo de IVA**\* · **Régimen fiscal**\* · **Cuenta contable**\* + totales de la línea.
- Tipos de IVA (venta): Exento 0% · General 21% · No Sujeto 0% · Reducido 10% · Reducido mínimo 7,5% · Reducido mínimo 5% ·
  Super Reducido 4% · Súper reducido mínimo 2% (+ Gestionar lista).
- Al cambiar el IVA salta aviso "Cambiar tipo de IVA — El cambio del tipo de IVA afecta al régimen fiscal asociado".
- **Régimen fiscal = código de impuesto** (tabla Grupo · Código · Régimen). Para General 21% en ventas:
  C0038 Entrega de bienes de inversión · C0043 Operaciones sujetas con derecho a devolución · C0044 Ventas con recargo de equivalencia ·
  C0045 Ventas régimen general · C0099 Modificación de bases y cuotas por concurso o crédito incobrable.
  ⇒ Cada línea queda clasificada para los modelos (303/390) y libros de IVA sin intervención del usuario.
- Cuenta contable: lookup del PGC a 9 dígitos filtrado por grupo (70x/706/708…), con + Crear.

## Presupuesto (diferencias)
- Campo "Fecha de presupuesto\*", "Prefijo".
- **Cliente opcional**: permite presupuestar a un **contacto potencial** con campos en línea Razón social o nombre · Nombre · E-mail ·
  Teléfono · País\*. (El cliente se crea al convertir.)
- Dashboard muestra "Presupuestos pendientes" y "Presupuestos convertidos en otro documento de venta" + "Preparar recordatorios".

## Pedido / Albarán (diferencias)
- Cliente\* obligatorio, "Fecha de pedido\*"/"Fecha de albarán\*", columna **% IVA** visible en la línea.

## Factura recurrente
- Crear abre primero el panel **Programación de facturas recurrentes**: Empieza el\* · Termina (Nunca · En una fecha · Tras n.º repeticiones) ·
  Frecuencia\* (Diariamente · Semanalmente · Mensualmente · Anualmente · El primer día de cada mes · El último día de cada mes ·
  El último viernes de cada mes · **Personalizada** → Repetir cada N [Meses…] · El\* [Día…] · Día [1-31]).
- **Resumen de recurrencia** en lenguaje natural: "Tus facturas se van a crear el día 16 de cada mes a partir del 16/10/2026 y sin fecha de fin."
- Origen "Factura recurrente" filtrable en el listado de facturas.

## Pendiente de observar (requiere un documento emitido; no se ha creado ninguno en la cuenta real)
- Acciones de una factura emitida (enviar por e-mail con plantilla, PDF, duplicar, rectificar, registrar cobro, convertir).
- Numeración final al emitir vs. borrador y comportamiento de VeriFactu/QR.
- Conversión presupuesto → pedido → albarán → factura.
Recomendación: probarlo en una empresa de pruebas de Sage o pedir a Sergio permiso para crear/borrar un borrador.
