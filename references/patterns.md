# Catálogo de patrones + Linter de anti-patrones

## Parte A — Patrones canónicos (reconocer la firma, aplicar el molde)

No improvises estructura: identifica la firma del proceso y usa el patrón.

| Patrón | Firma estructural | Cuándo aplica | Molde |
|---|---|---|---|
| **Secuencia** | A→B→C | Pasos obligatorios sin decisión | Cadena lineal |
| **Bifurcación XOR** | split → ramas → merge | "Depende de…" | Gateway XOR abre, gateway XOR cierra |
| **Paralelismo AND** | fork → ‖ → join | Tareas simultáneas independientes | Gateway AND abre y cierra (obligatorio el join) |
| **Inclusivo OR** | una o más ramas → join OR | Varias condiciones no excluyentes | Gateway OR abre y cierra |
| **Reproceso / Reintento** | back-edge con guarda de salida | "Si falla, volver a…" | Loop con gateway que tiene rama de escape + contador/límite |
| **Aprobación** | enviar → revisar → [aprob → sigue][rechazo → loop al autor] | Validaciones con autoridad | XOR tras revisión; rama rechazo vuelve atrás |
| **Escalamiento** | resolver → ¿puedo? → [no → subir nivel] | Soporte, excepciones jerárquicas | XOR que deriva a otro lane superior |
| **Guarda previa** | check → [no cumple → fin][sí → continúa] | Pre-condiciones / validación de entrada | XOR temprano, rama negativa a fin |
| **Excepción / Compensación** | try → catch → deshacer/compensar | Manejo de errores con rollback | Evento de error intermedio → sub-flujo de compensación |
| **Espera / Polling** | loop con timer hasta condición | Procesos asíncronos | Evento timer intermedio + XOR de condición |
| **Productor–Consumidor** | cola/buffer entre dos lanes | Desacople, batch | Almacén entre lanes + flujo mensaje |
| **Máquina de estados** | transiciones por status | Ciclos de vida (pedido, ticket) | Usar Mermaid `stateDiagram-v2`; en BPMN, eventos por estado |

### Heurística de selección
1. ¿Hay decisión? No → Secuencia. Sí → ¿excluyente? XOR. ¿simultáneo? AND.
2. ¿Hay vuelta atrás? → Reproceso / Aprobación / Escalamiento según quién retoma.
3. ¿Hay espera por tiempo o evento externo? → Espera/Polling o gateway por evento.
4. ¿Hay error que requiere deshacer trabajo? → Excepción/Compensación.
5. ¿El proceso es "qué le pasa a una entidad" más que "qué hace un actor"? →
   Máquina de estados.

## Parte B — Linter de anti-patrones (pasada P6, corregir antes de renderizar)

### Conectividad
- ❌ **Nodo colgante**: actividad/gateway sin flujo de salida (salvo eventos Fin).
- ❌ **Agujero negro**: nodo con entrada pero sin salida que no es un Fin.
- ❌ **Milagro**: nodo con salida pero sin entrada que no es un Inicio.
- ✅ Regla: **1 solo Inicio** por pool; **≥1 Fin**; todo nodo **alcanzable** desde
  el inicio y capaz de **alcanzar un fin**.

### Decisiones
- ❌ **Rama de gateway sin etiqueta**.
- ❌ **Decisión no-MECE**: ramas que se solapan o que no cubren todos los casos
  (falta el "else"/"No").
- ❌ **Gateway AND/OR sin su join** correspondiente.

### Loops
- ❌ **Loop sin condición de salida** (riesgo de bucle infinito).
- ✅ Todo back-edge pasa por un gateway con rama de escape explícita.

### Carriles / handoffs
- ❌ **Cruce de carril sin evento de handoff** explícito.
- ✅ Cada transferencia entre lanes/pools es visible (flujo o evento mensaje).

### Abstracción y limpieza
- ❌ **Mezcla de niveles** (una tarea atómica junto a un macro-proceso).
- ❌ **>7±2 elementos por nivel** → descomponer en sub-proceso.
- ❌ **Spaghetti**: aristas que se cruzan → re-rutear ortogonal o reordenar nodos.
- ❌ **Etiquetas inconsistentes**: tareas que no empiezan con verbo, decisiones
  que no son preguntas.

### Balance (de los PFD)
- ✅ Todo input declarado se consume; todo output declarado tiene origen.
- ✅ Ningún dato/almacén queda desconectado del flujo que lo usa.

## Checklist final (reportar al usuario qué pasó)
```
[ ] 1 inicio, ≥1 fin, todos los fines son estados reales del proceso
[ ] Todo nodo es alcanzable y alcanza un fin
[ ] Gateways XOR son MECE y con ramas etiquetadas
[ ] Forks AND/OR tienen su join
[ ] Loops tienen condición de salida
[ ] Handoffs entre lanes son explícitos
[ ] Un solo nivel de abstracción; ≤7±2 nodos o descompuesto
[ ] Sin aristas cruzadas; ruteo ortogonal
[ ] Etiquetas: verbo en tareas, pregunta en decisiones
[ ] Leyenda presente
```
