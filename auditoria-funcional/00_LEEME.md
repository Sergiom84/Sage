# Auditoría funcional de Sage Active (es.active.sage.com)

- **Fecha:** 2026-10-16.
- **Autor:** Claude (sesión Sage).
- **Para:** cotejar con la auditoría de Codex y con F-Gestor-IA (repo clonado en `/Users/sergio/Desktop/Aplicaciones/GFiscal`).

## Método y límites
- **Navegación como usuario** en el Chrome de Sergio, con la sesión ya iniciada: pantallas, formularios, desplegables, menús, mensajes y
  validaciones. **No se ha extraído código fuente, bundles ni respuestas de API de Sage.**
- **No se ha guardado, creado, borrado ni enviado nada.** Los formularios se abrieron y se descartaron con "Cambios sin guardar → Sí".
  Los informes solo se generaron en modo consulta.
- **Sin pulsar:** Conectar banco, Configurar VeriFactu, Configurar pagos en línea, Descargar plantilla y Consentimientos API (piden login
  o consentimiento). El chat de Copilot no se usó.
- **Privacidad:** la cuenta tiene datos reales de un negocio y de las empresas cliente de la asesoría. No se copian nombres, NIF, importes
  ni e-mails, solo estructura. Por eso `capturas/` está vacía: las capturas mostraban datos reales.
- **Plan auditado:** *Sage Active Starter*. No incluye contabilidad, asientos ni modelos en el menú; la asesoría los lleva en *Sage Despachos*.
  Las pantallas de configuración contable sí están (plan de cuentas, diarios, tipos impositivos, ejercicios).
- **Sin observar** (no hay ventas emitidas en la cuenta): acciones sobre una factura ya emitida (envío, PDF final, rectificar, cobrar, QR VeriFactu)
  y la conversión presupuesto → factura. Para verlas haría falta una empresa de pruebas, o que Sergio autorice crear y borrar un borrador.

## Índice
| Fichero | Contenido |
|---|---|
| `01_navegacion.md` | Menús, rutas `/list/…` `/page/…` `/menu-page/…`, patrones comunes de listados |
| `modulos/01_cuadro_de_mando_y_shell.md` | Dashboard, novedades, barra superior, tareas, usuarios y roles, auditoría, suscripción, ayuda |
| `modulos/02_ventas.md` | Presupuestos, pedidos, albaranes, facturas y recurrentes: formulario completo, detalle contable por línea, condiciones de pago |
| `modulos/03_compras.md` | Bandeja OCR, estados, revisión en vista partida, IVA por línea, registrar pago, e-mail de compras |
| `modulos/04_contactos.md` | Fichas de cliente y proveedor (todas las pestañas), importación de terceros, 17 categorías de compra |
| `modulos/05_productos.md` | Productos, unidades, precios, tarifas y grupos de descuento |
| `modulos/06_bancos.md` | Conciliación, 10 reglas de automatización con su editor, cuentas de banco y caja |
| `modulos/07_informes.md` | Vencimientos, antigüedad, VeriFactu (registro y eventos), libro registro, ficheros, exportaciones |
| `modulos/08_configuracion.md` | Los 24 apartados: numeración, VeriFactu, cuentas por defecto, diarios, **tipos impositivos y regímenes C00xx**, plan de cuentas, categorías, plantillas PDF y de e-mail, formas de pago… |
| `80_inventario_F-Gestor-IA.md` | Inventario funcional de tu app (lectura del repo) |
| `90_matriz_comparativa.md` | Sage frente a F-Gestor-IA por área, con estado y prioridad |
| `91_oportunidades.md` | Dónde ya ganas, errores de Sage a evitar y backlog P0/P1/P2 |

## Los 5 hallazgos más importantes
1. **El corazón de Sage es la tabla de tipos impositivos × régimen fiscal (códigos C00xx)**, asignada a cada línea de factura mediante
   **categorías** en lenguaje de negocio. Eso alimenta libros, modelos y autorrepercusión. F-Gestor-IA no lo tiene: es el P0 número 1.
2. **VERI\*FACTU** está preparado en Sage (tres modos, huellas, eventos oficiales, XML), con obligación desde el 01/01/2027. En F-Gestor-IA
   está desconectado de las facturas de venta.
3. **La numeración se asigna al finalizar** (borrador sin número definitivo) y la estructura de serie es configurable. En F-Gestor-IA el número
   se asigna en el borrador, lo que puede dejar huecos.
4. **La IA de Sage falla con el recargo de equivalencia** y varias categorías contables por defecto están mal. Ahí puede ganar F-Gestor-IA,
   cuya IA documental ya es más rica.
5. **Sage Starter no tiene contabilidad**: el negocio paga Starter y la asesoría paga Despachos. F-Gestor-IA ya integra la contabilidad,
   y ese es el argumento para dejar de pagar a Sage.
