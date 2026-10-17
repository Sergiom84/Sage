# Traspaso: cruzar la auditoría de Claude con la de Codex

Fecha del traspaso: 2026-10-16.

## Objetivo
Sergio (gestoría) quiere dejar de pagar Sage Active Starter + Sage Despachos y quedarse con su propia app, **F-Gestor-IA**, a la
altura de Sage o mejor. Claude y Codex auditaron Sage Active en paralelo. Ahora toca **cruzar las dos auditorías**, compararlas con
F-Gestor-IA y sacar **una lista única de huecos priorizada**.

## Rutas
| Qué | Dónde |
|---|---|
| Auditoría de Claude (hecha) | `/Users/sergio/Desktop/Aplicaciones/Sage/auditoria-funcional/` |
| App de Sergio (repo clonado) | `/Users/sergio/Desktop/Aplicaciones/GFiscal` (github.com/Sergiom84/F-Gestor-IA) |
| Auditoría de Codex | **Pedírsela a Sergio** (no se conoce la ruta) |
| Herramienta de ingeniería inversa (MCP `rea`) | `/Users/sergio/Desktop/Aplicaciones/REA`. No hace falta para esta fase |
| BD y Render | En la configuración de July, si se necesitan más adelante |

## Qué contiene la auditoría de Claude (leer en este orden)
1. `00_LEEME.md`: método, límites, índice y los 5 hallazgos clave.
2. `90_matriz_comparativa.md`: Sage frente a F-Gestor-IA por área (✅ 🟡 ❌ ⭐ y prioridad P0/P1/P2).
3. `91_oportunidades.md`: dónde F-Gestor-IA ya gana, errores de Sage que no hay que copiar y backlog P0/P1/P2.
4. `80_inventario_F-Gestor-IA.md`: inventario funcional de la app, con rutas de ficheros.
5. `modulos/01…08_*.md`: detalle por pantalla (campos, desplegables, estados, reglas, cuentas, códigos C00xx). Se consultan solo cuando hay
   una discrepancia.

## Reglas que hay que respetar
- **Solo comparación funcional.** No extraer ni reutilizar código, bundles ni respuestas de API de Sage. Si la auditoría de Codex incluye
  código de Sage, se usa solo como referencia de comportamiento y no se copia nada a F-Gestor-IA.
- **La cuenta de Sage es real** (datos de un negocio y de las empresas cliente de la asesoría). No guardar, crear, borrar ni enviar nada.
  Si hay que verificar algo en Sage, se abre el formulario y se descarta con "Cambios sin guardar → Sí". Ojo: en los desplegables de Sage,
  Escape selecciona la opción resaltada; para cerrar, hacer clic fuera.
- **No copiar datos personales** (nombres, NIF, importes, e-mails) a los documentos.
- Contexto del plan: la cuenta es **Sage Active Starter** (sin menú de contabilidad); la contabilidad la lleva la asesoría en Sage Despachos.

## Hallazgos de Claude que hay que contrastar con Codex
1. Motor fiscal de Sage: **tipos impositivos (18, con vigencia y % RE) × régimen fiscal con código C00xx**, asignados por línea mediante
   **17 categorías de compra** → cuenta PGC + régimen. Autorrepercusión 472/477 en intracomunitarias e ISP.
2. **VERI\*FACTU**: tres modos (tiempo real, por requerimiento, otro), huellas encadenadas, eventos 01-10/90, XML; obligatorio desde el 01/01/2027.
3. **Numeración al finalizar** (prefijo, número, ejercicio, separador, relleno de ceros, último número utilizado); factura simplificada con aviso a partir de 400 €.
4. **10 reglas de conciliación** (4 acciones, hasta 6 condiciones, tolerancias ±2 días y ±2 €, contador de usos).
5. Errores de Sage: la IA confunde el recargo de equivalencia; SaaS a la 206; cursos a la 623; intereses bancarios a la 662 "empresas del grupo";
   plantillas de e-mail en inglés y sin variables.

**Sin observar** (no había ventas emitidas): acciones sobre una factura emitida (envío, PDF final, rectificar, cobrar, QR VeriFactu) y la
conversión presupuesto → factura. Ver si Codex lo cubrió.

## Pasos para la nueva conversación
1. Pedir a Sergio la ruta de la auditoría de Codex y leerla entera.
2. Leer `00_LEEME.md`, `90_matriz_comparativa.md` y `91_oportunidades.md` de Claude.
3. Construir el cruce en `auditoria-funcional/95_cruce_claude_codex.md`, con cuatro tablas:
   - **Coincidencias**: los dos vieron lo mismo.
   - **Solo Codex**: hallazgos que Claude no tiene, con la evidencia de Codex.
   - **Solo Claude**: hallazgos que Codex no tiene.
   - **Contradicciones**: datos distintos (campos, valores por defecto, cuentas, estados). Para cada una, decidir cuál es correcta con la
     evidencia disponible; si no basta, marcarla "verificar en Sage (solo lectura)".
4. Verificar contra el código de GFiscal cada hueco nuevo que aporte Codex (`grep` en `app/`, `src/` y `supabase/migrations/`), para no
   dar por ausente algo que ya existe.
5. Sacar `auditoria-funcional/96_backlog_unificado.md`: lista única P0/P1/P2, deduplicada, con origen (Claude, Codex o ambos) y fichero de
   GFiscal afectado.
6. Proponer el siguiente paso: plan de implementación de los P0 en GFiscal (empezando por el motor de impuestos y regímenes).

## Prompt para pegar en la nueva conversación
```
Lee /Users/sergio/Desktop/Aplicaciones/Sage/SIGUIENTE_CONVERSACION.md y síguelo. La auditoría de Codex está en: <RUTA>.
Cruza ambas auditorías con F-Gestor-IA (/Users/sergio/Desktop/Aplicaciones/GFiscal) y genera 95_cruce_claude_codex.md y
96_backlog_unificado.md en /Users/sergio/Desktop/Aplicaciones/Sage/auditoria-funcional/. Solo comparación funcional; no toques nada en Sage.
```
