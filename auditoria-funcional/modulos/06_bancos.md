# Bancos — Movimientos bancarios, Automatización bancaria, Cuentas bancarias o efectivo

Rutas: `/list/bank-transaction` (Movimientos) · `/list/payment-method` (Cuentas bancarias o efectivo).

## Movimientos bancarios (conciliación)
- Cabecera: título + icono de ayuda (?) · **Actualizar propuestas** · Configuración ▾ → **Automatización bancaria**.
- Texto: "Concilia los movimientos bancarios para comprobar lo que se ha pagado y mantener los registros al día."
- Banner cerrable "Puntos clave": *Cuenta bancaria conectada* (importación automática a "Por conciliar") · *Revisión y conciliación*
  (aceptar propuestas con "Conciliar" o crearlas si no existen) · *Bajo control* (si no hay propuesta, buscar en registros, vincular o
  crear transacción "bajo el nombre del revisor"; **se puede revertir la vinculación**) · *Datos fiables*.
- Filtros: **Cuenta bancaria** (lookup) + tarjetas **Saldo bancario** e **Importe sin conciliar** · Fecha inicio/fin · Desde/Hasta importe · buscador · Filtrar.
- Pestañas: **Por conciliar** (badge) · **Conciliados** · **Omitidos**.
- Rejilla de dos bloques: *Movimientos bancarios* (Fecha · Concepto · Importe) ↔ *Transacciones propuestas* (Tipo · Tercero · Propuesta) ·
  **Conciliar** · Acciones.

## Automatización bancaria (reglas)
- Panel "Define reglas para automatizar las propuestas durante la conciliación."
- Selector de cuenta + KPIs **Reglas activas** / **Reglas totales**. Botón **Crear regla** · ☐ Mostrar reglas inactivas · buscador · Filtrar.
- Columnas: Estado · Cuentas bancarias · Nombre · Condiciones ("Esta regla tiene N condiciones.") · Creada por · **Regla aplicada**
  ("0 veces desde el 03/03/2026" → contador de uso) · Editar · Acciones.
- **10 reglas de serie creadas por "Sage Copilot"**:
  - Creación de transacción para pagos de tarjetas de crédito (1 condición: Concepto contiene "Tarjeta").
  - Creación de transacción para cuotas de préstamo.
  - Creación de transacción para pagos de alquiler y arrendamiento.
  - Creación de transacción para pagos de nómina.
  - Creación de transacción para comisiones bancarias y de mantenimiento.
  - Coincidencia por fecha exacta (2) · por importe exacto (2) · por importe y fecha exactos (2).
  - Coincidencia por nombre comercial (3: Concepto *contiene* [campo de datos: Nombre comercial] · Fecha *dentro del intervalo* ±2 días de la
    fecha de transacción · Importe *dentro del intervalo* ±2,00 €).
  - Coincidencia por número de factura (3).
- **Editor de regla:** Nombre\* · ¿A qué cuentas? (Todas / Una específica) · **Acción\***:
  Proponer coincidencia con transacción existente · Proponer nueva transacción para cobro de tercero · Proponer nueva transacción para pago a
  tercero · Proponer nueva transacción sin relación con tercero.
  **Condiciones** (hasta 6): Campo\* (Concepto de movimiento, Fecha de movimiento, Importe de movimiento…) · Criterios\* (Contiene, Dentro del
  intervalo…) · Tipo\* (Valor fijo / Campo de datos / Fecha de transacción / Importe de movimiento) · Valor o tolerancia (días ±, euros ±).
  **Detalles de transacción** (para reglas de creación): Categoría (Ingreso financiero · Interés de deuda con institución de crédito · Otra ·
  Pago con tarjeta de crédito · Pago de IVA · Pago de nómina · Retirada de efectivo · Servicios bancarios y similares…) · Motivo\* (cuenta,
  p. ej. "Préstamos a C/P de entidades de crédito"). ☐ Desactivar regla.

## Cuentas bancarias o efectivo
- Tarjetas por cuenta: nombre, saldo, cuenta contable (`572000000` banco / `570000000` caja), "Última actualización",
  botones **Conectar** (open banking), Editar, Eliminar. Botón global **Sincronizar todo**.
- Alta (panel): Tipo\* (Cuenta bancaria / Efectivo) · Nombre\* · **Diario** (BNC) · Cuenta contable (572… Bancos e instituciones de crédito c/v) ·
  IBAN · Banco (se deduce del IBAN) · BIC/SWIFT · Divisa (EUR) · Inactiva.
- Las formas de pago (Configuración) apuntan a estas cuentas; el "Registrar pago" de compras elige entre ellas.
- No se pulsó "Conectar" (abre la conexión con el banco/agregador; requiere consentimiento del titular).
