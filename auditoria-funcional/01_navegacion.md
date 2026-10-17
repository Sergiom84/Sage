# Navegación y estructura general

## Shell de la aplicación
- **Barra superior:** logo (vuelve a home del portal Sage `app.sbc.sage.com`), Inicio, Notificaciones (campana),
  Tareas (desplegable), Mi perfil (desplegable), selector de empresa (nombre de la empresa activa, desplegable),
  Ayuda, **Copilot** (asistente IA de Sage).
- **Menú lateral fijo (iconos + texto)**, con flyout de submenú al hacer clic en los que llevan flecha:

| Menú | Submenú | Ruta observada |
|---|---|---|
| Cuadros de mando | — | `/` (home) |
| Ventas ▸ | Presupuestos · Pedidos · Albaranes · Facturas · Facturas recurrentes | `/list/sales-offer`, `/list/sales-invoice`, … |
| Compras | (directo) Facturas de compra | `/list/simplified-purchase-invoice` |
| Contactos ▸ | Clientes · Proveedores | |
| Productos y servicios ▸ | Productos y servicios · Precios y descuentos (grupo desplegable) | |
| Bancos ▸ | Movimientos bancarios · Bancos | |
| Informes | (directo) | |
| Configuración | (directo) | |

Nota: en este plan/rol **no aparece un módulo "Contabilidad"** en el menú (ni diario, ni mayor, ni modelos), aunque las
facturas muestran el estado "La factura está contabilizada": la contabilidad existe por detrás (probablemente la gestiona
la asesoría desde Sage Active para despachos o un rol con más permisos). Ver Configuración para confirmarlo.

## Patrones de URL
- `/list/<entidad>` → listados (p. ej. `sales-invoice`, `sales-offer`, `simplified-purchase-invoice`).
- `/page/<pantalla>` → pantallas de consulta/informes (p. ej. `dead-line-payment`, `aging-balance`).
- Todas llevan `bid` (id de empresa/negocio) y `tid` (id de tenant) en la query → multiempresa por URL.
- Parámetros de informe en query, p. ej. aging con tramos `firstDeadline=30&secondDeadline=45&thirdDeadline=60`
  y `thirdPartyType=1` (clientes) / `2` (proveedores).

## Patrones de UI comunes en listados
- Cabecera con título + botón **Copilot Insights** (IA contextual a la pantalla).
- Botón primario **Crear**, buscador, botón **Filtrar** (panel), **Personalizar** → *Columnas* (mostrar/ocultar y
  reordenar con "Mover", "Restablecer valores por defecto") y *Altura de fila*.
- Pestañas de estado con contador (badge "99+").
- Columnas **Editar** (lápiz) y **Acciones** (menú) fijas a la derecha.
- Pie con "Elementos: N".
- Estado vacío: "Esta lista está en blanco. La búsqueda no ha dado ningún resultado."
