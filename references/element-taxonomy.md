# Taxonomía de elementos BPMN 2.0 + estilos draw.io

Cada elemento tiene **semántica estricta**, **regla de uso** y **estilo draw.io
exacto**. El estilo va en el atributo `style` de un `<mxCell vertex="1">`.

## 1. Eventos (círculos) — *algo pasa*

| Elemento | Semántica | Regla | Estilo draw.io |
|---|---|---|---|
| **Inicio** | Disparador del proceso | Exactamente **1** por pool | `ellipse;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;` |
| **Inicio mensaje** | Inicia al recibir mensaje | Variante de inicio | `shape=mxgraph.bpmn.shape;perimeter=mxPerimeter.ellipsePerimeter;html=1;outline=standard;symbol=message;` |
| **Inicio timer** | Inicia por tiempo/calendario | Variante de inicio | `shape=mxgraph.bpmn.shape;perimeter=mxPerimeter.ellipsePerimeter;html=1;outline=standard;symbol=timer;` |
| **Intermedio** | Espera / mensaje / timer en el flujo | Solo si interrumpe o espera | `ellipse;whiteSpace=wrap;html=1;fillColor=#ffe6cc;strokeColor=#d79b00;strokeWidth=2;` |
| **Fin** | Estado terminal (puede haber varios) | **≥1**, borde grueso | `ellipse;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;strokeWidth=3;` |
| **Fin error** | Termina por error | Variante de fin | `shape=mxgraph.bpmn.shape;perimeter=mxPerimeter.ellipsePerimeter;html=1;outline=end;symbol=error;fillColor=#f8cecc;strokeColor=#b85450;` |

Tamaño recomendado: 50×50 (eventos), centrados verticalmente con las tareas (que
son 60 de alto → offset +5px).

## 2. Actividades (rect. redondeado) — *se hace trabajo* → etiqueta = VERBO

| Elemento | Semántica | Regla | Estilo |
|---|---|---|---|
| **Tarea** | Acción atómica | Verbo + objeto ("Validar pedido") | `rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;` |
| **Tarea usuario** | La hace una persona | Ícono persona | `shape=mxgraph.bpmn.shape;perimeter=mxPerimeter.rectanglePerimeter;html=1;outlineConnect=0;label=Usuario;fillColor=#dae8fc;strokeColor=#6c8ebf;`... usar tarea normal si no hay set BPMN |
| **Tarea sistema/auto** | La ejecuta un sistema | Gris = sin intervención humana | `rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;` |
| **Sub-proceso** | Bloque colapsado (otro nivel) | Marca `+`, descompone complejidad | `rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;` |

Tamaño recomendado: 120×60.

## 3. Gateways (rombo) — *el flujo se decide* → etiqueta = PREGUNTA

| Elemento | Semántica | Regla | Estilo |
|---|---|---|---|
| **Exclusivo (XOR)** | Un solo camino | Ramas **MECE**, todas etiquetadas | `rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;` |
| **Paralelo (AND)** | Todos los caminos a la vez | Fork **debe** tener join | `shape=mxgraph.bpmn.gateway;gwType=parallel;html=1;fillColor=#fff2cc;strokeColor=#d6b656;` |
| **Inclusivo (OR)** | Uno o más caminos | Usar con cuidado, requiere join | `shape=mxgraph.bpmn.gateway;gwType=inclusive;html=1;fillColor=#fff2cc;strokeColor=#d6b656;` |
| **Basado en evento** | Espera el primer evento que ocurra | Seguido de eventos intermedios | `shape=mxgraph.bpmn.gateway;gwType=eventBased;html=1;fillColor=#fff2cc;strokeColor=#d6b656;` |

Tamaño recomendado: 50×50. Si no se dispone del set `mxgraph.bpmn`, usar `rhombus`
y poner el símbolo (`+`, `O`) como texto.

## 4. Conexiones — *cómo se relacionan* (`<mxCell edge="1">`)

| Elemento | Semántica | Estilo |
|---|---|---|
| **Flujo secuencia** | Orden de ejecución | `edgeStyle=orthogonalEdgeStyle;rounded=0;html=1;endArrow=block;` |
| **Flujo condicional** | Sale de un gateway con condición | Igual + etiqueta de rama (Sí/No/…) |
| **Flujo por defecto** | Rama default del gateway | `edgeStyle=orthogonalEdgeStyle;startArrow=dash;endArrow=block;html=1;` |
| **Flujo mensaje** | Cruza pools (comunicación) | `edgeStyle=orthogonalEdgeStyle;dashed=1;startArrow=oval;startFill=0;endArrow=block;endFill=0;html=1;` |
| **Asociación** | Liga artefacto/dato a un paso | `edgeStyle=orthogonalEdgeStyle;dashed=1;endArrow=none;html=1;` |

Regla: toda arista que sale de un gateway exclusivo **lleva etiqueta**.

## 5. Carriles y artefactos

| Elemento | Semántica | Estilo |
|---|---|---|
| **Pool** | Participante/proceso completo | `swimlane;html=1;horizontal=0;startSize=23;fillColor=none;` |
| **Lane** | Rol dentro del pool | `swimlane;html=1;horizontal=0;startSize=23;fillColor=none;` (anidado, `parent`=pool) |
| **Dato** | Input/output de información | `shape=note;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#666666;` |
| **Almacén (BD/tabla)** | Repositorio persistente | `shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;` |
| **Anotación** | Comentario aclaratorio | `shape=mxgraph.bpmn.shape;perimeter=mxPerimeter.rectanglePerimeter;html=1;symbol=general;fillColor=none;` o texto con borde izquierdo |
| **Grupo** | Agrupación lógica (no afecta flujo) | `rounded=1;dashed=1;html=1;fillColor=none;strokeColor=#999999;` |

`horizontal=0` en pool/lane pone el título vertical a la izquierda (orientación
L→R del flujo). Para flujo T→B usar `horizontal=1`.

## Paleta semántica (memorizar)

| Color fill / stroke | Significado |
|---|---|
| `#d5e8d4` / `#82b366` (verde) | Inicio |
| `#f8cecc` / `#b85450` (rojo) | Fin / Error / Almacén crítico |
| `#dae8fc` / `#6c8ebf` (azul) | Tarea (humana/negocio) |
| `#f5f5f5` / `#666666` (gris) | Tarea automática / sistema |
| `#fff2cc` / `#d6b656` (ámbar) | Gateway / decisión |
| `#e1d5e7` / `#9673a6` (morado) | Sub-proceso |
| `#ffffff` / `#666666` (blanco) | Dato |
| `#ffe6cc` / `#d79b00` (naranjo) | Evento intermedio / espera |
