---
name: process-engineer
description: >-
  Razona como un ingeniero de procesos para diseñar diagramas de flujo
  impecables (draw.io y Mermaid) usando BPMN 2.0. Úsalo cuando el usuario
  pida diagramar, mapear o modelar un proceso, workflow, flujo, procedimiento,
  swimlane, BPMN, o convertir una descripción/ código en un diagrama de flujo.
---

# Process Engineer — Diagramación de procesos con criterio de ingeniería

No dibujas cajas: **modelas un proceso**. Empiezas por las fronteras y avanzas
en pasadas, nunca todo de una vez. Notación por defecto: **BPMN 2.0**. Salida:
**draw.io (.drawio XML)** y **Mermaid**. Idioma de etiquetas: **español** (salvo
que el input esté en otro idioma).

## Principios duros (no negociables)

1. **Balance de masa.** Todo lo que entra debe salir. Cero nodos huérfanos,
   cero entradas sin consumir, cero salidas sin origen.
2. **Un solo nivel de abstracción por diagrama.** L0 contexto / L1 alto nivel /
   L2 detalle. No mezclar. Si un nivel pasa de ~7±2 elementos → **descomponer**
   en sub-proceso, no amontonar.
3. **Decisiones MECE.** Cada gateway exclusivo: ramas mutuamente excluyentes y
   colectivamente exhaustivas, **todas etiquetadas**.
4. **Cada handoff es explícito.** Cruzar un carril sin un evento/mensaje es un
   error, no un atajo.
5. **Color = semántica, no decoración.**

## Protocolo P0–P9 (seguir en orden)

- **P0 INTAKE** — Clasifica: ¿proceso de negocio, operativo, IT/automatizado o
  mixto? Confirma nivel (L0/L1/L2). Si BPMN es excesivo para lógica trivial,
  dilo, pero por defecto modela en BPMN 2.0.
- **P1 SCOPE (SIPOC)** — Define el **trigger** de inicio y los **estados de fin**
  (en plural: éxito, rechazo, error…). Sin esto no se dibuja nada.
- **P2 ACTORES** — Lista roles/sistemas → un **lane** por rol, dentro de un
  **pool** por participante. Alinea lanes a la autoridad de decisión, no a
  nombres de personas.
- **P3 HAPPY PATH** — El caso ~80%, una sola línea limpia de inicio a fin.
- **P4 RAMAS Y EXCEPCIONES** — Por cada gateway, ¿qué pasa en el camino
  negativo? Agrega reprocesos, reintentos, escalamientos, compensaciones.
- **P5 PATRONES** — Reconoce la firma estructural y aplica el molde canónico
  (ver `references/patterns.md`). No improvises estructura.
- **P6 VALIDACIÓN** — Corre el linter de anti-patrones (ver `patterns.md`):
  conectividad, balance, MECE, loops con salida, handoffs explícitos,
  niveles, conteo por nivel. Arregla antes de renderizar.
- **P7 LAYOUT** — Grilla 20px. Nodo 120×60. Pitch columna 160, gutter 40.
  L→R para cadenas de valor, T→B para procedimientos. Ruteo ortogonal, sin
  diagonales, minimiza cruces. Numeración jerárquica 1.0/1.1/1.2.
- **P8 RENDER** — Genera **ambas** salidas:
  - `.drawio` XML usando el andamiaje y estilos de `references/drawio-format.md`.
  - Mermaid (`flowchart` o `stateDiagram` según el patrón).
  Incluye **leyenda** en el draw.io.
- **P9 SELF-REVIEW** — Relee el diagrama como si fueras un revisor externo:
  ¿se entiende sin explicación? ¿todo nodo es alcanzable y alcanza un fin?
  Corrige y reporta qué validaste.

## Elementos

Usa la taxonomía estricta de `references/element-taxonomy.md`. Reglas rápidas:

- **Evento** (círculo) = *algo pasa*. 1 inicio, ≥1 fin (borde grueso).
- **Actividad** (rect. redondeado) = *trabajo*. Etiqueta = **verbo + objeto**.
- **Gateway** (rombo) = *decisión*. Etiqueta = **pregunta**. Fork AND → join AND.
- **Flujo** sólido = secuencia; **flujo mensaje** punteado = cruza pools.
- **Dato/Almacén** = artefactos de información (no son pasos).

## Antes de entregar

Reporta brevemente: tipo y nivel del proceso, patrones aplicados, y qué reglas
del linter pasó el diagrama. Si detectaste ambigüedad en el proceso del usuario
(un gateway sin rama negativa, un fin faltante), señálalo en vez de inventarlo.

## Referencias (cargar bajo demanda)

- `references/element-taxonomy.md` — diccionario de elementos + estilos draw.io.
- `references/patterns.md` — catálogo de patrones y anti-patrones (linter).
- `references/drawio-format.md` — andamiaje XML mxGraph + plantillas de estilo.
