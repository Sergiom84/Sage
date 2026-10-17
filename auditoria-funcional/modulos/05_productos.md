# Productos y servicios · Tarifas · Grupos de descuentos

Rutas: `/list/product`, `/page/product` · `/list/sales-tariff`, `/page/sales-tariff` · `/list/sales-discount-group`.
Submenú: Productos y servicios · Precios y descuentos ▾ (Tarifas · Grupos de descuentos).

## Listado de productos
- Botones: **Importar productos y servicios** · Configuración ▾ · Crear · Acciones en bloque · buscador · Filtrar · Personalizar.
- Columnas: Código · Nombre · Categoría · Fecha de alta · **Precio con descuento** · Estado · Editar · Eliminar.

## Ficha de producto/servicio
Pie fijo con **Precio** y **Precio con IVA y descuento** recalculados en vivo.
### Pestaña Información básica
- Categoría (radio): Producto / Servicio.
- Código\* · Nombre\* · **Unidad de medida** (Gramo g · Kilogramo kg · Kilómetro km · Litro l · Metro m · Metro cuadrado m² ·
  No aplica · Unidad uds.) · Fecha de alta (hoy) · Inactivo (toggle).
- **Grupo de impuestos\*** (por defecto "General – 21 %").
- Descripción (2.500 caracteres, contador) · Comentarios internos (250 caracteres).
### Pestaña Precios y descuentos de venta
- **Definición de precio unitario:** Precio · Porcentaje de descuento · Importe de descuento (calc.) · Precio con descuento (calc.) ·
  Cuota de impuesto (calc.) · Precio con IVA y descuento (tarjeta).
- **Cuenta contable** (por defecto `700000000 – Ventas de mercaderías`).
- Tabla **Tarifas** en las que está el producto: Código · Nombre · Tipo de ajuste · Fecha inicio/fin · Estado · Valor de ajuste · **Tramos** · Ver.
- Tabla **Grupos de descuentos**: Código · Nombre · Fechas · Estado · % descuento a cliente · Tramos · Ver.
- **Gestión de documentos de venta:** Bloquear pedidos / albaranes / facturas para este producto.

## Tarifas
- Listado: Código · Nombre · Fecha de inicio · Fecha de fin · Tipo de ajuste · Activa · Editar · Eliminar.
- Formulario: Código\* · Nombre\* · **Tipo de ajuste\*** (Precio fijo · Incremento porcentual · Importe de incremento) ·
  Fecha de inicio · Fecha de fin · Activa (toggle).
- Rejilla de productos de la tarifa: Código de producto o servicio · Nombre · Unidad de medida · Activa · **Tramos** · Editar · Eliminar + Añadir.
- La tarifa se asigna al cliente (Condiciones de venta) y se hereda en el documento (pestaña Información de cliente).

## Grupos de descuentos
- Listado: Código · Nombre · Fecha de inicio · Fecha de fin · Activo · Editar · Eliminar.
- Misma mecánica que tarifas, pero con % de descuento por cliente y tramos.
