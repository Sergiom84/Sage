# Cuadro de mando, barra superior y portal Sage Business Cloud

## Contexto de la cuenta auditada
- Plan: **Sage Active Starter** (Gestionar cuenta empresarial → Suscripciones). Por eso el menú no muestra Contabilidad, Asientos,
  Declaraciones ni informes financieros: la contabilidad la lleva una **asesoría con Sage Despachos** (exportación de asientos +
  Tenant/Business ID). Las "Novedades" confirman que en planes superiores existen **asientos** y su eliminación/navegación en bloque.
- El usuario que entra es de la asesoría y ve **varias empresas cliente** en el selector (multiempresa de despacho).

## Cuadro de mando (`/`)
- Saludo "Hola, <nombre>" + **Copilot Insights** + "Sage Active actualiza tus KPI cada 5 minutos".
- Pestañas: **Ventas y compras** · **Novedades**.
- Ventas y compras:
  - *Importes pendientes*: **Pendiente de cobro** (barra + total, "Ver vencimientos", "Ver antigüedad de saldos") y **Pendiente de pago**
    (barra con "Importe vencido" en naranja + total; mismos enlaces con `thirdPartyType=2`).
  - KPIs: total facturas de venta contabilizadas (ejercicio en curso) · total facturas de compra contabilizadas · Clientes activos.
  - **Accesos rápidos**: Crear clientes · Crear proveedores · Crear facturas de venta · Subir facturas de compra.
  - **Facturas de venta vencidas** (tabla Estado · Fecha · Número · Cliente · Código · Total · Acciones) + Ver todas + **Preparar recordatorios**.
  - **Presupuestos pendientes** (total, nº convertidos en otro documento, tabla) + Ver todos + Preparar recordatorios.
- Novedades (changelog dentro de la app, sept. 2026): Eliminación en bloque (documentos de venta, productos, servicios, **asientos**, cuentas
  contables; notificación al terminar) · App móvil iOS/Android con QR · **Facturas simplificadas para particulares** (sin DNI; cliente genérico o
  individual) · **Smart Split** de PDFs de compra (revisar y ajustar los cortes antes de generar cada PDF) · **Navegación rápida** entre registros
  respetando filtros y orden · Portal de ideas con votos · Release notes.

## Barra superior
- **Inicio** · **Notificaciones** (popover "Estás al día" + Ver todas) · **Tareas** ▾ (Ver tareas · Añadir tarea) · **Mi perfil** ▾ (Mi perfil · Cerrar sesión) ·
  **Selector de empresa** ▾ (Gestionar cuenta empresarial · Gestionar usuarios · OTRAS EMPRESAS…) · **Ayuda** · **Copilot**.
- Ayuda y soporte (panel lateral "con tecnología de Sage Copilot"): buscador "¿Con qué necesitas ayuda?", recomendaciones contextuales
  (Personaliza el diseño de tus documentos · Pagos en línea · Recopilatorio sobre VeriFactu…), botón **Chat**, aviso legal de IA.

## Portal Sage Business Cloud (`app.sbc.sage.com`, compartido por todos los productos Sage)
- Conmutador "Volver al producto / CAMBIAR DE PRODUCTO" (aquí solo "Active").
- **Tareas**: pestañas Lista de tareas · Configuración de productos (checklist de onboarding con % completado) · Tareas completadas;
  filtros rápidos Todas · Atrasadas · Por completar pronto · Nuevas · Vencen pronto; "Mostrar solo mis tareas"; orden por vencimiento y prioridad;
  **vista en listas / vista en columnas (kanban)**. Alta en 2 pasos: Título\* (100) · Fecha de vencimiento\* · Marcar como prioritaria · Descripción
  enriquecida → (paso 2: asignación).
- **Gestionar usuarios**: pestañas Usuarios · Niveles de permisos · Invitaciones pendientes · **Registro de actividad de cuenta**.
  - Usuario: acceso a nivel de cuenta (Gestionar suscripciones · Gestionar usuarios) + acceso a nivel de empresa (tabla Nivel de permisos ·
    Producto · Empresa · **Último acceso**). Botón Añadir (invitación).
  - **4 niveles de permisos fijos**:
    - *Administrador*: informes de terceros; gestionar datos generales; importar cuentas y asientos; **exportar datos de auditoría fiscal**; gestionar
      empresas; terceros; instalar/desinstalar apps API; importar productos; gestionar cuentas bancarias.
    - *Contable*: gestionar terceros e importación; ver datos generales; informes de terceros; importar asientos y cuentas; gestionar cuentas
      bancarias; ver empresas.
    - *Administrador de ventas y compras*: ver cuentas bancarias; gestionar clientes, proveedores e importación; importar productos; informes de terceros;
      ver datos generales y empresas.
    - *Usuario de solo lectura*: ver proveedores, clientes, terceros importados, datos generales, informes de terceros, empresas, cuentas bancarias.
  - **Registro de actividad**: periodo (Últimos 7 días…), buscador, filtros, orden; cada evento con Fecha · Hora · Usuario · Actividad ·
    **Valor original** · **Valor nuevo** · Tipo de actividad (p. ej. Acceso de usuario).
- **Gestionar cuenta empresarial**: Datos de empresa (razón social, dirección, provincia, país, web, teléfonos) · Suscripciones · **Uso** ·
  Datos de pago y facturación · Facturas (de Sage al cliente).
