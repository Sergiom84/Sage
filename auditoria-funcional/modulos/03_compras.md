# Compras — Facturas de compra

Ruta listado: `/list/simplified-purchase-invoice` · Detalle: `/page/simplified-purchase-invoice?id=<uuid>` ·
Alta manual: `/page/simplified-purchase-invoice` (sin id).
El nombre interno "simplified" importa: la factura de compra es **por cabecera + desglose de IVA**, no por líneas de artículo.

## Listado
- Cabecera: título + **Copilot Insights** + botón **Ver dirección de e-mail**.
- Texto guía: "Selecciona Crear… También puedes subir ficheros o enviar las facturas a la dirección de e-mail de tu usuario".
- **Banner "Formas más rápidas de registrar tus compras"** (cerrable con ⓧ), 3 tarjetas:
  1. *Registro de documentos desde el e-mail* — bandeja de entrada de compras; extracción automática y "listos para su revisión".
  2. *División automática de PDF con varias facturas* — **Smart Split** detecta inicio/fin de cada factura y separa el fichero.
  3. *Tus documentos, siempre contigo* — fotos/subida desde app móvil iOS/Android.
- **Zona drag&drop** "Seleccionar fichero o arrastrarlo hasta aquí" (subida directa desde el listado). Acepta PDF e imágenes (hay filas `.jpg` de fotos de móvil).
- Botón **Crear** (alta manual), buscador, **Filtrar**, **Personalizar** (Columnas / Altura de fila).
- **Pestañas:** Todas · Por revisar (badge) · Por pagar (badge) · Pagadas.
- **Columnas por defecto:** Fecha de importación · Nombre de fichero · Estado · Descripción · Proveedor (orden ↑ por defecto) ·
  Fecha de factura · Número de factura · Total · Editar · Acciones.
- **Columnas opcionales:** Importe pendiente · Fecha de vencimiento · Fecha de creación · Fecha de operación · Páginas de documentos.
- **Filtros (fila bajo la cabecera, por columna):** fecha con operador (Igual a, …) + datepicker `dd/MM/yyyy`; texto; Estado con
  multiselección + buscador + "(Seleccionar todo)" + "Restablecer filtro".
- **Estados (chips de color):** Vencida (rojo) · Pagada (verde) · Parcialmente vencida (rojo) · Parcialmente pagada (azul) ·
  Pendiente (gris) · Por pagar (azul) · Error de fichero (rojo) · Subiendo (azul).
- **Columna Descripción** = mensaje de estado del procesamiento: "La factura está contabilizada.", "Los datos se han extraído. …".
- **Acciones de fila:** pendiente → solo *Eliminar*; contabilizada → sin acciones (inmutable).
- Pie: "Elementos: N".

## Bandeja por e-mail
- Panel lateral "Facturas de compra por e-mail": dirección única por usuario `<alias>-facturascompra@ai.sage.com`,
  botones **Copiar** y **Editar** (alias editable). "Los documentos enviados a esta dirección se extraen y clasifican
  automáticamente. Esto incluye PDF, imágenes y varios ficheros adjuntos." · "Comparte esta dirección con tus proveedores."

## Detalle / revisión (vista partida)
- **Izquierda:** visor del documento original. Para PDF: visor con miniaturas, paginación `1/1`, zoom (%), rotar, anotar texto,
  dibujar, descargar, imprimir, menú ⋮. Para fotos: imagen.
- **Derecha:** formulario extraído por IA:
  - **Proveedor** (lookup) → muestra automáticamente la **dirección de facturación** del proveedor.
  - Número de factura · Fecha de factura · Fecha de operación · Total.
  - **Tabla IVA** (rejilla editable inline): Impuesto · Base imponible · Cuota de IVA · **Categoría** · Acciones (⋮).
    Botón **+ Añadir** inserta una fila nueva con IVA 21% por defecto y categoría por defecto.
  - ⋮ de línea → **Ver detalles contables** (panel): *Tipo de IVA*\*, *Régimen fiscal*\* (p. ej. "Compras bienes y servicios
    corrientes régimen general"), *Cuenta contable*\* (9 dígitos, p. ej. 600000000 – Compras de mercaderías) + totales de la línea
    (Base / Cuota / Total de línea).
- **Cabecera de la página:** chip de estado, **Ver información técnica** (IDs de soporte: Orchestration ID, Customer unique ID,
  Unique ID + "Copiar detalles"), **Ver comentarios** (hilo de comentarios internos por documento: "Añade un comentario para
  mantener a tu equipo al día"), flechas **anterior/siguiente** para recorrer la bandeja sin volver al listado.
- **Borrar todo** (vacía los campos extraídos).
- **Pie de acciones:**
  - Pendiente: Cancelar · Actualizar (split button con más opciones) · **Contabilizar**.
  - Contabilizada: Cancelar · Actualizar (deshabilitado) · **Registrar pago**.
  - Alta manual: Cancelar · **Crear** (split button).
- Al salir con cambios: modal "Cambios sin guardar — ¿Quieres descartarlos? No / Sí".
- Campos bloqueados (gris) cuando la factura está contabilizada.

## Catálogo de impuestos en compras (desplegable "Impuesto")
Columnas Nombre · Tipo impositivo: IVA 0% · IVA 10% · IVA 2% · IVA 21% · IVA 4% · IVA 7,5% · IVA mínimo 5% · No Sujeto · Tipo 0
+ enlace **Gestionar lista** (catálogo editable).
**No aparece recargo de equivalencia** como línea. Hallazgo real: en una factura con RE 1,4% la IA de Sage lo mal-clasificó como
"IVA mínimo 5%" y descuadró la base del 10%. → Oportunidad: detectar RE y validar `base × tipo = cuota` por línea.

## Categorías (asignación contable por línea)
Se ven, entre otras: "Compras (IVA general del 21 %)", "Compras a países de la UE". La categoría arrastra tipo de IVA +
régimen fiscal + cuenta contable → es la **plantilla contable** que evita que el usuario elija cuentas.

## Registrar pago (modal)
- Texto: "Selecciona una fecha de pago y la cuenta desde donde lo has realizado. Introduce el importe total pagado … para poder
  seleccionar los vencimientos y realizar el marcaje."
- Campos: **Fecha de pago**\* (hoy por defecto) · **Cuenta bancaria o efectivo**\* (lookup: "Cuenta bancaria por defecto",
  "Efectivo por defecto") · **Importe por registrar**\* (pendiente por defecto).
- **Tabla de vencimientos**: ☑ · Fecha de vencimiento · Número de factura · Importe · Importe pendiente · **Importe por registrar**
  (editable → pago parcial) · Estado.
- **Descripción de asiento** (texto por defecto "El asiento se ha generado a partir del pago.").
- Totalizador "Importe total registrado" · Cancelar · Confirmar (deshabilitado hasta completar obligatorios).
- ⇒ el pago genera asiento y **marcaje** (punteo) del vencimiento.

## Patrón de lookup (se repite en toda la app)
Desplegable tipo tabla con columnas (Código · Razón social o nombre · Nombre comercial), búsqueda al teclear, y pie con
**Gestionar lista** (abre el maestro) y **+ Crear** (alta rápida sin salir del formulario).

## Copilot Insights (Compras)
Panel "Sage Copilot" → tarjeta "Insights – No hay insights por ahora", feedback 👍/👎, aviso legal "Verifica la información…
no constituye asesoramiento profesional". En esta cuenta no aporta valor.
