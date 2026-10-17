# Contactos — Clientes y Proveedores

Rutas: `/list/customer`, `/page/customer` · `/list/supplier`, `/page/supplier`.

## Listados
- Botones: **Importación de terceros** · Crear · Acciones en bloque · buscador · Filtrar · Personalizar.
- Columnas: Código · Razón social o nombre · Nombre comercial · Número de identificación · Editar · Eliminar.
- Códigos de proveedor con ceros a la izquierda (`000010`); los importados conservan su código de origen.

## Importación de terceros (asistente a pantalla completa)
- Botones **Requisitos previos** · **Guía de importación** · ⋮ → **Descargar plantilla**.
- Modal "Requisitos previos de importación": *Cuentas contables — las cuentas que falten se generan automáticamente a partir de la
  información encontrada en la importación. También las puedes importar antes…* [Añadir cuentas] · Más información ·
  ☐ No volver a mostrar esta pantalla.
- Zona "Arrastra el fichero hasta aquí / o abre el explorador de ficheros" (CSV).
- **Historial de importaciones**: Fecha · Nombre de fichero · Estado (chip "Importado") · Descripción ("Todos los registros se han importado.") ·
  **Líneas importadas** · **Líneas por importar** · Acciones (⋮ → Mostrar terceros importados · Mostrar fichero CSV de origen · Eliminar fichero).

## Ficha de cliente (pantalla completa, ✕ para cerrar)
- **Banner de aviso**: "Tipo de cliente necesario para la facturación electrónica — selecciona Empresa o Particular".
- **KPI arriba a la derecha:** "Importe vencido" del cliente.
- **Pestañas:** Información · Contactos · Condiciones de pago · Direcciones · Condiciones de venta.

### Información
- **Tipo de cliente** (radio): *Empresa* (sociedades, autónomos y otras organizaciones) / *Particular* (consumidores privados).
- Código (autonumérico, gris) · Razón social o nombre\* · Nombre comercial · País (por defecto ES) · Tipo de identificación
  (derivado del país: "NIF/DNI/NIE", gris) · Número de identificación · NIF-IVA · **Idioma** (de los PDF) · **Código CNAE** ·
  **Recargo de equivalencia** (toggle) · **Categoría** (maestro libre; vacío → "Crea un nuevo elemento").
- **Dirección principal** (tarjeta + Editar) y **Contacto principal** (tarjeta + Editar).
- **Información contable:** Cuenta contable (por defecto `430000000 – Clientes (euros)`) · Cuenta contable para anticipos
  (por defecto `438000000 – Anticipos de clientes`).
- **Información adicional:** Comentarios · **Notas finales de factura** (texto legal por cliente) · toggle **Inactivo**.
- Crear (split) deshabilitado hasta completar obligatorios.

### Contactos
- Lista de personas de contacto + Añadir.

### Condiciones de pago
- Condiciones de pago (plantilla; por defecto "En efectivo") · **Forma de pago** (Domiciliación bancaria · Efectivo · Tarjeta de crédito ·
  Cheque · Transferencia — cada forma enlazada a una "Cuenta bancaria o efectivo"; + Gestionar/Crear) · **Días de pago de cliente**.
- Lista de vencimientos: "1.er vencimiento — Importe restante — A pagar después de 0 días" [Editar] [Eliminar] + Añadir.

### Direcciones
- Lista de direcciones adicionales. Panel **Dirección**: Referencia ("Dirección principal") · Dirección · Línea 2 · País ·
  **Búsqueda de códigos postales o ciudades** (autocompleta CP/ciudad/provincia) · Código postal · Ciudad · Provincia ·
  ✅ "Esta dirección se utiliza como dirección de entrega por defecto."

### Condiciones de venta
- Código/Nombre de tarifa · Código/Nombre de grupo de descuentos · % descuento a cliente.
- **Gestión de documentos de venta:** toggles **Bloquear facturas** / **Bloquear albaranes** / **Bloquear pedidos**
  ("No se van a poder crear … para este cliente").

## Ficha de proveedor
- Pestañas: Información · Contactos · Condiciones de pago (sin Direcciones ni Condiciones de venta).
- KPI "Importe vencido".
- Información: Código · Razón social\* · Nombre comercial · País · Tipo de identificación · Número · NIF-IVA · Código CNAE ·
  **Tipo** (maestro libre).
- **Información contable:**
  - Cuenta contable (por defecto `400000000 – Proveedores (euros)`).
  - **Categoría de compra** (por defecto "Compras (IVA general del 21 %)") → es la **categoría que la IA aplica a sus facturas**.
  - **IRPF** (toggle) → al activarlo aparece **Régimen fiscal\*** con: `1 General` · `2 Profesionales de nuevo inicio` ·
    `3 Arrendamiento o subarrendamiento de bienes inmuebles urbanos` (+ Gestionar lista) ⇒ alimenta 111 / 115.
- Información adicional: Comentarios · Inactivo.

## Catálogo de categorías de compra (17, lenguaje de negocio, no contable)
Alquileres de oficinas, equipos y vehículos · Anuncios, web, logotipos y folletos · Compra de máquinas industriales ·
Compra de ordenadores, pantallas y periféricos · Compras a países de la UE · Compras (IVA general del 21 %) ·
Compras (IVA reducido del 10 %) · Compras (IVA superreducido del 4 %) · Compras sin IVA · Consultoría, asesoría legal y gestoría ·
Cursos y talleres para empleados · Facturas de luz, gas y otros suministros · Gasolina, billetes, hoteles y comidas ·
Materiales de oficina, consumibles, herramientas pequeñas y embalajes · Programas, licencias y aplicaciones en la nube ·
Revisiones, reparaciones y acondicionamientos · Teléfono, seguridad, limpieza y otros servicios externos.
(+ Gestionar lista / + Crear). Cada categoría = cuenta PGC + tipo de IVA + régimen fiscal (ver Compras > Detalles contables).
Las de inversión (máquinas, ordenadores) implican inmovilizado (21x) en lugar de gasto (6xx).
