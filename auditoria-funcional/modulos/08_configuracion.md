# Configuración

Ruta: `/menu-page/settings` — página-menú agrupada en 10 bloques y 24 apartados:

| Bloque | Apartados |
|---|---|
| Empresa | Gestión de empresa · Números de secuencia |
| Cumplimiento normativo | Verificación antifraude de facturas |
| Contabilidad | Configuración de contabilidad · Plan de cuentas · Diarios · Ejercicios · Tipos impositivos |
| Bancos | Automatización bancaria |
| Categorías | Categorías bancarias · Categorías de compra · Categorías de inmovilizado |
| Ventas y compras | Ventas y compras · Preferencias de documentos · Productos y servicios · Plantillas de e-mail |
| Contactos | Condiciones de pago · Formas de pago · Departamentos |
| Importaciones | Importación de terceros · de productos y servicios · de cuentas contables |
| Sage Marketplace | Aplicaciones de partners |
| API pública | Claves de aplicación · Consentimientos |

## Gestión de empresa (`/page/organization`)
- Pestañas: **Información** · **Contactos** · **Obligaciones legales**.
- Información: Razón social o nombre\* · Número de identificación · NIF-IVA · **Forma jurídica** (lista oficial AEAT por clave de NIF:
  Asociación, Comunidad de bienes/herencias yacentes, Comunidad de propietarios, Congregación religiosa, Corporación local, Entidad extranjera,
  Establecimiento permanente de no residentes, … Persona física nacional, SA, SL…) · Código CNAE · Dirección (tarjeta + Editar) · Contacto principal.
- **Obligaciones legales → Retención de IRPF**: toggle "Habilitar retención de IRPF — se aplicará a los documentos de venta" +
  **Régimen fiscal** (Capital inmobiliario: Arrendamiento… · Carácter general: General · Nuevo inicio: Profesionales de nuevo inicio).
  ⇒ El IRPF de ventas es una propiedad **del emisor**, no del cliente ni de la línea.

## Números de secuencia (`/list/operational-number-counter`)
- Tabla por Módulo/Entidad: Ventas → Presupuesto · Pedido · Albarán · Factura; General → Cliente · Proveedor. Columnas: Cantidad (nº de series) ·
  Primer elemento · Separador · Segundo elemento · Separador · Tercer elemento · Acciones (Gestionar números de secuencia · Editar estructura).
- **Editar estructura** ("facturas y notas de abono" comparten estructura): hasta 3 elementos (**Prefijo · Número · Ejercicio · Sin especificar**),
  separadores (**Ninguno · Guion · Barra baja · Barra · Punto · Espacio**), "Autocompletar con ceros a la izquierda" + Longitud de número (4).
- **Gestionar números** (`/list/operational-number-counter-management`): Prefijo · Descripción · Prefijo por defecto · Estado · **Vista previa** ·
  Ejercicio · **Último número utilizado** · Editar · Eliminar. Alta: Prefijo · Descripción · Ejercicio\* · Último número utilizado\* (permite continuar
  una numeración traída de otro programa) · Vista previa en vivo · ☐ Desactivar prefijo · ☐ Definir prefijo por defecto.

## Verificación antifraude de facturas (`/page/organization-verifactu-setup`)
- Banner: "A partir del 01/01/2027 será obligatorio tener configurado al menos un sistema de verificación de facturas."
- Tres opciones: **VeriFactu o presentación en tiempo real** (Recomendado; "Sage Active envía directamente a la AEAT los datos XML") ·
  **Presentación por requerimiento** (XML guardado para enviarlo cuando la AEAT lo pida; = NO VERI\*FACTU) · **Otro sistema de verificación**
  (no obligado o usa otro sistema). Enlace "Más información sobre VeriFactu". En esta cuenta **no está configurado**.

## Configuración de contabilidad (`/page/organization-accounting-setup`)
| Parámetro | Valor por defecto |
|---|---|
| Longitud de cuentas | 9 (botón **Ampliar longitud**) |
| Cuenta de cliente / anticipo de cliente / proveedor | 430000000 / 438000000 / 400000000 |
| Ventas a clientes nacionales / intracomunitarios / fuera UE | 700000000 (los tres, configurables por separado) |
| Impuestos soportados / repercutidos | 472000000 / 477000000 |
| Cuenta de banco / caja | 572000000 / 570000000 |
| Diario de caja / banco | CJ / BNC |

## Diarios (`/list/journal-type`)
Código · Nombre · Tipo · Inactivo: APT Apertura (Apertura) · BNC Banco (Financiero) · CIE Cierre (Cierre) · CJ Caja (Financiero) ·
COM Facturas de compra · GEN General · RECOM Facturas rectificativas de compra · REVEN Facturas rectificativas de venta · VEN Facturas de venta.

## Ejercicios (`/list/accounting-exercise`)
Ejercicio · Descripción · Fecha de inicio · Fecha de fin · Estado (Abierto…). 2025 y 2026 abiertos.

## Tipos impositivos (`/list/tax`) — vista maestro/detalle
**18 tipos**: IRPF 15% (Carácter general) · IRPF 19% (Capital inmobiliario) · IRPF 7% (Nuevo inicio) · IVA 0% (Exento) · IVA 10% (Reducido) ·
IVA 10% + RE 1,4% · IVA 2% (Súper reducido mínimo) · IVA 21% (General) · IVA 21% + RE 5,2% · IVA 2% + RE 0,26% · IVA 4% (Super reducido) ·
IVA 4% + RE 0,5% · IVA 5% + RE 0,62% · IVA 7,5% · IVA 7,5% + RE 1% · IVA mínimo 5% · No Sujeto · Tipo 0.
- Cabecera de detalle: Tipo de impuesto · Porcentaje · Grupo · **Fecha de vigencia** (p. ej. 01/09/2012) · **% recargo de equivalencia** · Inactivo.
- **Tabla de regímenes fiscales por tipo** (ej. IVA 21% + RE 5,2%): Régimen · Tipo (Compras/Ventas) · **Código de impuesto** · Cuenta soportado ·
  Cuenta repercutido · **Inversión de sujeto pasivo** · Inactiva.

| Código | Régimen | C/V | 472 | 477 | ISP |
|---|---|---|---|---|---|
| C0031 | Compras bienes de inversión régimen general | C | ✔ | | |
| C0032 | Compras bienes y servicios corrientes régimen general | C | ✔ | | |
| C0033 | Compras intracomunitarias de bienes | C | ✔ | ✔ | ✔ |
| C0034 | Compras intracomunitarias de bienes de inversión | C | ✔ | ✔ | ✔ |
| C0035 | Compras intracomunitarias de servicios | C | ✔ | ✔ | ✔ |
| C0036 | Compras inversión del sujeto pasivo | C | ✔ | ✔ | ✔ |
| C0037 | Compras ISP bienes de inversión | C | ✔ | ✔ | ✔ |
| C0006 | Importaciones bienes de inversión | C | ✔ | | |
| C0029 | Importaciones bienes y servicios corrientes | C | ✔ | | |
| C0098 | Modificación de bases y cuotas por concurso o créditos incobrables | C | ✔ | | |
| C0038 | Entrega de bienes de inversión | V | | ✔ | |
| C0043 | Operaciones sujetas con derecho a devolución | V | | ✔ | |
| C0044 | Ventas con recargo de equivalencia | V | | ✔ | |
| C0045 | Ventas régimen general | V | | ✔ | |
| C0099 | Modificación de bases y cuotas por concurso o créditos incobrables | V | | ✔ | |
(Los códigos cambian por tipo: p. ej. corrientes al 10% = C0076, al 4% = C0107, sin IVA = C0122.)
**Autorrepercusión**: en intracomunitarias e ISP el mismo régimen apunta a 472 **y** 477 → asiento doble automático.
- **IRPF 15%** → régimen General: Compras → *Cuenta de retenciones practicadas* 475100000 (HP acreedora por retenciones practicadas);
  Ventas → *Cuenta de retenciones soportadas* 473000000 (HP retenciones y pagos a cuenta).

## Plan de cuentas (`/list/accounting-account`)
- **1.427 cuentas** (PGC completo). Botones Importar cuentas contables · Crear · Acciones en bloque · Filtrar.
- Columnas: Código · Nombre · **Nivel** (Grupo · Subgrupo · Cuenta · Desglose · Subcuenta) · **Naturaleza** · **Tipo** (Balance de situación / PyG) ·
  Código de impuesto · **Saldo** · Inactiva · Editar · Eliminar.
- Panel de cuenta: pestañas **Identificación** (Código\* · Nombre\* · Nivel · Tipo · Naturaleza · Inactiva) · **Terceros relacionados** ·
  **Informes financieros** ("posición de la cuenta en los informes": p. ej. Balance de situación > Sección principal > 1. Capital escriturado).
  Pie con Saldo · Total debe · Total haber.
- **Naturalezas**: Clientes · Proveedores · Banco · Efectivo · Gastos · Ingresos · Capital · Inmovilizado · Empleados · Otras cuentas (balance) ·
  Anticipos de clientes · Anticipos a proveedores · Impuestos soportados · Impuestos repercutidos · Envases y embalajes a devolver a proveedores.

## Categorías bancarias (`/list/category`)
- Banner: finalidad (explicar movimientos sin tercero, comisiones, descuadres de cambio), uso personalizado (transferencias internas, nóminas;
  categorías de **ajuste** para pequeños descuadres), "Revisa el asiento conciliado — se crea un asiento simplificado; pide a tu contable que lo revise".
- Pestaña **Transacciones**: Ingreso financiero 769 · Interés de deuda con institución de crédito **662** · Otra 555 (por defecto) ·
  Pago con tarjeta de crédito 520 · Pago de IVA 4750 · Pago de nómina 465 · Retirada de efectivo 570 · Servicios bancarios 626. Columna Impuesto (0%).
- Pestaña **Ajustes**: Ganancia cambiaria 768 · Otra 555 (por defecto) · Pérdida cambiaria 668.
- ⚠ Error de Sage: "Interés de deuda con institución de crédito" apunta a 662000000 "Intereses de deudas, **empresas del grupo**" (debería ser 6623).

## Categorías de compra (`/list/category?purchase`) — Categoría → Cuenta → Régimen fiscal
| Categoría | Cuenta | Régimen |
|---|---|---|
| Alquileres de oficinas, equipos y vehículos | 621 Arrendamientos y cánones | C0032 |
| Anuncios, web, logotipos y folletos | 627 Publicidad | C0032 |
| Compra de máquinas industriales | 213 Maquinaria | C0031 (inversión) |
| Compra de ordenadores, pantallas y periféricos | 217 Equipos proceso información | C0031 |
| Compras a países de la UE | 600 Compras de mercaderías | C0033 (intracom.) |
| Compras (IVA general del 21 %) | 600 | C0032 |
| Compras (IVA reducido del 10 %) | 600 | C0076 |
| Compras (IVA superreducido del 4 %) | 600 | C0107 |
| Compras sin IVA | 600 | C0122 |
| Consultoría, asesoría legal y gestoría | 623 Servicios profesionales | C0032 |
| Cursos y talleres para empleados | 623 | C0032 |
| Facturas de luz, gas y otros suministros | 628 Suministros | C0032 |
| Gasolina, billetes, hoteles y comidas | 629 Otros servicios | C0032 |
| Materiales de oficina, consumibles, herramientas pequeñas y embalajes | 602 Otros aprovisionamientos | C0032 |
| Programas, licencias y aplicaciones en la nube | **206 Aplicaciones informáticas** | C0032 |
| Revisiones, reparaciones y acondicionamientos | 622 Reparaciones | C0032 |
| Teléfono, seguridad, limpieza y otros servicios externos | 629 | C0032 |
⚠ Incoherencias de Sage: SaaS/"aplicaciones en la nube" va a **206 (inmovilizado)** con régimen de *corrientes* (C0032); lo correcto para
suscripciones es 629 (gasto). Los cursos a 623 en lugar de 649.

## Categorías de inmovilizado (`/list/fixed-asset-category`)
21 categorías con Código · Nombre · Tipo (Intangible / Material) · Cuenta contable:
INTANGINVESTIG 200 · INTANGDESSARRO 201 · INTANGCONCES 202 · INTANGPATENT 203 · INTANGFONDOC (sin cuenta) · INTANGDERECHTRAS 205 ·
INTANGINFORM 206 · INTANGDERECHEMGAS 207 · INTANGANTICIP 209 · INTANGPROPINTELECT (sin cuenta) · MATTERRENOS 210 · MATCONSTRUC 211 ·
MATINSTATECN 212 · MATMAQUIN 213 · MATUTILL 214 · MATOTRINSTAL 215 · MATMOBILIARO 216 · MATINFORM 217 · MATTRANSPORT 218 ·
MATOTRINMO 219 · MATINMOENCURSO 239.
Panel: Código\* · Tipo\* · Nombre\* · **Cuentas por defecto**: Cuenta contable · Cuenta de amortización · Cuenta de gastos de amortización ·
Cuenta de pérdidas. (No hay módulo de inmovilizado visible en el menú de este plan; las categorías existen para la asesoría.)

## Ventas y compras (`/page/organization-sales-setup`)
- **Preferencias de venta por defecto:** prefijo (serie) por defecto para facturas · facturas simplificadas · notas de abono · pedidos ·
  albaranes · presupuestos · ☑ Mostrar detalles de precios y descuentos en líneas de documentos.
- **Flujo de facturas de venta:** ☑ "Mostrar confirmación antes de finalizar — revisa los detalles más importantes cada vez que finalices" ·
  Diario por defecto\* (VEN) · Diario de notas de abono por defecto\* (VEN; existe REVEN pero no se usa por defecto).
  ⇒ Las facturas pasan de borrador a **finalizada** (emisión explícita), igual que facturas de anticipo y notas de abono.
- **Facturas simplificadas:** ☑ "Utilizar por defecto facturas simplificadas para particulares" (desactivable por cliente) ·
  **Aviso sobre importe límite**\* = 400,00 € (0 = sin aviso).
- **Flujo de facturas de compra:** Diario por defecto\* (COM) · ☑ "Mostrar confirmación de contabilizar".

## Preferencias de documentos (`/page/organization-sales-setup-docs-customization`) — diseñador de plantillas PDF
- **"Personaliza tus plantillas con Copilot":** subir un A4 (PDF/JPG/PNG ≤ 5 MB) y Copilot extrae su diseño.
- Acordeones:
  - *Logotipo de empresa* (PNG/JPG < 5 MB, 300×150 recomendado; tamaño Pequeño/Mediano/Grande).
  - *Diseño*: posición del logo (esquina sup. izq./dcha.) · datos de empresa (junto/debajo del logo) · dirección del cliente (izq./dcha.) ·
    descripción del producto (ancho de columna / ancho del documento).
  - *Estilo*: fuente (Source Sans Pro…), tamaño, color HEX · **paleta de color por tipo** (Facturas · Notas de abono · Albaranes · Pedidos ·
    Presupuestos · **Recibos de cobro**) o "Aplicar a todos" · imagen de fondo (≤ 10 MB, 1200×800; ajustar a alto/ancho; opacidad).
  - *Cuerpo* (por tipo de documento): Mostrar dirección de entrega en facturas · Mensaje personalizado por defecto (500) · columna de
    producto: Código / Nombre / Descripción.
  - *Notas finales y pie de página*: Notas finales (tras los totales) · Pie de página 1.ª y 2.ª línea (100 caracteres c/u).
- **Vista previa en vivo** con pestañas Factura · Nota de abono · Albarán · Pedido · Presupuesto + Descargar + Alejar/Acercar.

## Plantillas de e-mail (`/list/email-template`) — maestro/detalle
- 8 plantillas de serie (nombres internos en **inglés**, sin traducir): New quote (Nuevo presupuesto) · Send quote reminders (Recordatorio
  de presupuesto) · New order · New delivery note · New invoice · Recurring invoices templates · Send invoice reminders (Recordatorio de pago) ·
  Send invoice reminders (Recordatorio de próxima factura). Filtro por tipo + buscador + **Añadir plantilla**.
- Detalle: Renombrar · Eliminar · **Destinatarios** (☐ Enviarme una copia · ☐ copia a hasta 4 destinatarios separados por ";") ·
  Plantilla por defecto del tipo · **Asunto** · **Mensaje** con editor enriquecido (negrita, cursiva, subrayado, listas) y
  **Redactar con Copilot** (2.000 caracteres) · Actualizar · Guardar como plantilla nueva.
- No se ven **variables de combinación** ({cliente}, {número}, {importe}, {vencimiento}…): el texto es fijo.

## Productos y servicios (config) (`/page/organization-sales-setup-product-and-service`)
- **Unidades de medida** (Nombre · Abreviación · Categoría Productos/Servicios · **Decimales** · Activa): Día ds. (1) · Gramo g · Hora h ·
  Kilogramo kg · Kilómetro km · Litro l · Mes ms. (1) · Metro m · Metro cuadrado m² · No aplica (0) · Porcentaje % · Unidad uds. ·
  Metro cúbico m³ · Miligramo mg · Mililitro ml · Noche ns. (0) · Pack pks. (0) · Tonelada t.
- Unidades por defecto para Productos (Unidad) y Servicios · **Grupo de impuestos por defecto**\*.

## Condiciones de pago (`/list/payment-term`)
Nombre · Por defecto para clientes · Por defecto para proveedores: 50% ahora y 50% en 30 días · **En efectivo (defecto clientes y proveedores)** ·
Pago a 30 días · Pago a fin de mes.

## Formas de pago (`/list/payment-mean`)
- Banner **pagos en línea**: "Acelera tus cobros con pagos en línea desde las facturas" — configuración sencilla, enlace **"Pagar ahora"**
  en la factura (cobro por transferencia), comisión por transacción sin cuota mensual, cobros registrados automáticamente.
  [Configurar pagos en línea] (no pulsado).
- Formas con **código normalizado de medio de pago** (UNECE 4461, usado en factura electrónica): Domiciliación bancaria → 59 Adeudo directo SEPA ·
  Efectivo → 10 · Tarjeta de crédito → 48 Tarjeta bancaria · Cheque → 20 · Transferencia → 58 Transferencia SEPA. Estado Activa · Editar · Eliminar.

## Departamentos (`/list/job-area`)
Administración · Compras · Contabilidad · Dirección · Finanzas · Jurídico · Producción · Ventas (para clasificar contactos de terceros).

## Importaciones
Importación de terceros · de productos y servicios · de **cuentas contables** (mismo asistente: plantilla, guía, requisitos previos, historial).

## Sage Marketplace
Acceso a apps de partners por sector (enlace externo).

## API pública
- **Claves de aplicación** (`/backoffice/publicapi/applicationkeys`): aviso "solo para desarrolladores que quieran crear una aplicación con la API
  pública"; formulario de alta de desarrollador (Razón social\*, Estado, Nombre\*, Apellidos\*, E-mail\*, Dirección\*, CP\*, Ciudad\*, País\*…) +
  pestaña Aplicaciones. No se rellenó.
- **Consentimientos**: abre el portal de identidad de Sage (`id.sage.com`) en otra pestaña y pide login → no se accedió.
