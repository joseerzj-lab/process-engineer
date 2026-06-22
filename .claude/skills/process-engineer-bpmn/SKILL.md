---
name: process-engineer: bpmn-methodology
description: Ingeniería de Procesos con BPMN 2.0 — estándar OMG (ISO/IEC 19510). Cubre Niveles de Abstracción, 7PMG (Siete Directrices), Marco 3C (Corrección/Completitud/Claridad), Eventos de Frontera, Call Activities vs Subprocesos, y 15 Anti-patrones Rozman con soluciones. Use cuando diseñe/valide procesos BPMN, siga Método y Estilo, o audite calidad de diagramas.
---

# Ingeniería de Procesos: BPMN 2.0 Profesional

> Estándar OMG (ISO/IEC 19510) — Especificación 2.0.2 — Enfoque de Ingeniería de Sistemas

---

## Inicio Rápido: Selecciona Tu Nivel

### NIVEL 1: Descriptive — Visión Estratégica
```
Audiencia:       Directores ejecutivos, gestores de negocio
Enfoque:         Alcance global y objetivos estratégicos
Elementos:       Subconjunto simple (tareas, subprocesos básicos, pools, lanes)
Excepciones:     Omitidas — solo camino óptimo
KPIs:            Ciclos entrega, costos reclutamiento, tasas conversión
Rol Ingeniero:   Observador estratégico — análisis inicial
```

### NIVEL 2: Analytic — Optimización Operativa
```
Audiencia:       Analistas procesos, ingenieros calidad
Enfoque:         Mejora continua, simulación, optimización Lean Six Sigma
Elementos:       Paleta completa BPMN 2.0 (eventos, gateways, almacenes datos, frontera)
Excepciones:     Todas las rutas alternativas mapeadas
KPIs:            Tiempos espera, costos recursos, parámetros simulación
Rol Ingeniero:   Puente conceptual — traduce realidad operativa a modelo
```

### NIVEL 3: Executable — Automatización en Producción
```
Audiencia:       Desarrolladores, integradores, motores BPM
Enfoque:         Despliegue automático en motor ejecución
Elementos:       Service Tasks, Script Tasks, Business Rule Tasks, variables XML
Excepciones:     Transacciones, compensaciones, reintentos, reversión
KPIs:            Métricas en tiempo real (BI/Process Mining)
Rol Ingeniero:   Desarrollador integraciones — programación de scripts
```

---

## Las 7 Directrices de Modelado Empíricas (7PMG)

> Basadas en investigaciones de Mendling, Reijers & van der Aalst — correlación directa entre complejidad topológica y errores cognitivos

### Aplicar en Orden

| # | Directriz | Regla de Oro | Si Falla |
|---|-----------|-------------|----------|
| **G1** | Mínimos elementos | Use fewer elements in canvas | Sobrecarga cognitiva → +errores lógicos (correlación lineal) |
| **G2** | Bajo grado conexidad | Minimize routing paths per element | Riesgo exponencial de fallos lógicos en ejecución |
| **G3** | 1 inicio + 1 fin | Exactly one start/end event | Imposible validar soundness estructural formal |
| **G4** | Máxima estructura | Design as structured as possible (split/join simétricos) | Deadlocks permanentes, fragmentación hilos paralelos |
| **G5** | Sin gateways OR | Avoid inclusive gateways (OR) | Ambigüedad interpretativa, sincronización ultra-compleja |
| **G6** | Verbo-Objeto | Verb-Object labels ("Validar Crédito") | Confusión acción vs datos vs eventos vs áreas org |
| **G7** | Descomponer <=30 | Hierarchically decompose if >30 elements | Deterioro drástico comprensión → usar subprocesos |

Fuente científica: Correlación empírica validada entre tamaño modelo y propensión errores cognitivos

---

## Marco de Calidad 3C — Auditoría de Procesos

> Evalúa cada diagrama contra tres dimensiones con pesos ponderados

### Corrección | Peso: 3/3 (Crítico — Bloquea Ejecución)

```
Ausencia TOTAL de:
• Violaciones sintácticas (deadlocks, bucles infinitos)
• Errores estructurales (nodos desconectados)
• Violaciones semánticas (tipos tarea erróneos)
• Redundancia lógica sin valor
• Asimetría de gateways (split sin join)

Si falla: Modelo rechazado en motor BPM — bloqueo operativo
```

### Completitud | Peso: 3/3 (Crítico — Funcionalidad)

```
TODOS los elementos del requerimiento:
• Representados físicamente en diagrama
• Eventos inicio/fin explícitos (delimitan)
• Resultados lógicos gateways modelados (sí/no)
• Flujos excepción vía Boundary Events

Si falla: Omisión pasos críticos — desarrollo incompleto
```

### Claridad | Peso: 2-3/3 (Alto a Crítico — Usabilidad)

```
Diagrama autodescriptivo:
• Etiquetas correctas, sin inducir error
• Cero elementos sin etiquetar
• Espaciado limpio (sin zigzags, tamaños proporcionales)
• Mínimo cruce de flujos
• Condiciones XOR-split rotuladas claramente

Si falla: Fatiga visual → +errores lectura manual
```

---

## Subprocesos vs Call Activities — Diferencia Crítica

### Subproceso Embebido (Local)
```
Naturaleza:           Recurso visual de colapso DENTRO mismo contenedor XML
Variables datos:      Comparte IMPLÍCITAMENTE con proceso padre
Scope:                Lógica local, sin existencia autónoma
Reusabilidad:         NO — solo en este proceso
Mantenimiento:        Descentralizado por proceso
Uso:                  Organización visual, estructuración jerárquica
Mapeo E/S:            Automático (comparte contexto)
```

### Call Activity (Corporativa)
```
Naturaleza:           Invoca proceso EXTERNO definido en repositorio XML
Variables datos:      Mapeo EXPLÍCITO entrada/salida (aislamiento estricto)
Scope:                Proceso independiente, reutilizable
Reusabilidad:         SÍ — toda corporación
Mantenimiento:        Centralizado (cambios se propagan automáticamente)
Uso:                  Subprocesos estandarizados, gobernanza
Mapeo E/S:            Manual (bindings de variables)
```

### Regla de Método y Estilo (Bruce Silver)
> Significado lógico debe ser **unívoco y completamente comprensible del diagrama impreso**, sin consultar documentación adjunta.

---

## Eventos de Frontera (Boundary Events) — Manejo Asíncrono

Capturan desvíos del flujo principal operando en modo catching asíncrono:

### Interruptor (Trazo doble continuo)
```
Disparo:      Al activarse el trigger → cancela tarea INSTANTÁNEAMENTE
Destrucción:  Destructiva inmediata de ejecución bound
Token:        Desviado instantáneamente al flujo escape
Paralelo:     NO — reemplaza flujo original
Casos:        Timeouts críticos, cancelaciones, errores fatales
```

### No Interruptor (Trazo doble discontinuo)
```
Disparo:      Al activarse → clona token, inicia ruta paralela
Destrucción:  NO — tarea original continúa operando
Paralelo:     SÍ — ruta paralela independiente
Casos:        Alertas retraso, escaladas soporte, logs, monitoreo
Ejemplo:      Enviar email de alerta MIENTRAS se procesa orden
```

---

## Taxonomía: 15 Anti-patrones de Rozman & Polančič

> Investigación empírica: desviaciones recurrentes en modeladores inexpertos

| # | Anti-patrón | Categoría | Impacto Crítico | Solución |
|---|-------------|-----------|-----------------|---------|
| **1** | Actividades desconectadas en pool | Sintáctico | Parálisis hilos, estado no alcanzable | Enlazar todos elementos continuamente |
| **2** | Ausencia evento inicio | Pragmático | Incertidumbre origen caso | Incorporar evento inicio calificado |
| **3** | Ausencia evento fin | Pragmático | Estancamiento casos activos | Modelar eventos fin normales/terminación |
| **4** | Flujo cruzando subproceso | Sintáctico | Violación encapsulamiento jerárquico | Flujo solo por evento inicio subproceso |
| **5** | Flujo directo entre pools | Sintáctico | Error crítico estructural | Usar SOLO flujos mensaje entre pools |
| **6** | Gateway ejecutando mensaje | Semántico | Gateway solo enruta lógica, no ejecuta | Anteceder/suceder con Send/Receive Tasks |
| **7** | Evento frontera mal posicionado | Sintáctico | Fuera de borde actividad bound | Reposicionar sobre borde físico actividad |
| **8** | Elemento "colgado" sin salida | Sintáctico | Token se desvanece, caso sin conclusión | Enlazar hacia flujo secuencial o fin |
| **9** | Múltiples inicios redundantes | Pragmático | Sobrecarga cognitiva, mal interpretados | Consolidar 1 inicio, distribuir con gateways |
| **10** | Temporizador mal usado | Semántico | Retrasos severos o fallos síncronos | Estudiar semántica: relativo vs ISO 8601 |
| **11** | Flujos imitando datos | Semántico | Confusión control vs datos | Usar Data Objects, almacenes datos BPMN |
| **12** | Evento capturador como origen mensaje | Sintáctico | Incompatibilidad gramatical | Origen solo de Send Task/evento lanzador |
| **13** | Tareas genéricas en Executable | Semántico | Motor incapaz interpretar tipo tarea | Especificar: Manual, Usuario, Servicio, Script |
| **14** | Start Timer en secuencia | Sintáctico | Timer se instancia periódicamente autónomo | Reemplazar por evento intermedio capturador |
| **15** | Excepción sin controlador falla | Semántico | Excepciones huérfanas, sin recuperación | Conectar Boundary Event → tarea error |

Ver [REFERENCE.md](REFERENCE.md) para tabla completa con detalles técnicos

---

## Validación Automatizada — Herramientas Recomendadas

### Trisotech / Cameo Business Modeler
```
Detección en Tiempo Diseño:
- Reglas Método y Estilo precargadas
- Service Tasks sin mapeo parámetros
- Gateways decisión sin etiquetas condición
- Orquestaciones sobredimensionadas (>30 elementos)
```

### SpiffWorkflow
```
Motor Verificación Asíncrona:
- Análisis estáticos de Soundness (solidez)
- Validez técnica expresiones lógicas XOR/AND
- Pre-despliegue en producción
```

### Doble Filtro de Validación
```
1. VISUAL/ESTILO  →  Detecta violaciones sintácticas e inconsistencias
2. LOGICO/TECNICO →  Verifica comportamiento dinámico correcto
                 ↓
           Modelo LISTO PRODUCCIÓN
```

---

## Fundamentos Científicos

### Investigaciones Empíricas Base
- **Mendling, Reijers, van der Aalst**: Correlación topología vs errores cognitivos
- **Rozman, Polančič, Vajde Horvat**: Taxonomía 15 anti-patrones
- **John Krogstie (SEQUAL)**: Evaluación dimensiones físicas/empíricas/sintácticas/semánticas/pragmáticas
- **Bruce Silver (Método y Estilo)**: Principios BPMN-I, unívocidad, serialización XML estable

### Marcos Complementarios
- **Triple Corona OMG**: BPMN (orquestación) + CMMN (casos) + DMN (decisiones)
- **GoM (Guidelines of Modeling)**: Claridad, relevancia, comparabilidad, eficiencia, diseño sistemático
- **OMG OCEB 2**: Certificación profesional en 5 niveles progresivos

### SysCAD & Simulación Industrial
Para modelos simulación: define alcance, límites físicos, nivel detalle, variables ANTES de diseñar.
Principio GIGO: **Garbage In, Garbage Out** — calibración continua con datos reales operativos.

---

## Referencias Detalladas

Ver [REFERENCE.md](REFERENCE.md) para:
- Historia y evolución BPMN 2.0 (BPMI → OMG 2005 → Especificación 2.0.2)
- Relación UML vs BPMN (orientado objetos vs orientado procesos)
- Transición WS-BPEL → BPMN 2.0 native execution
- Tabla completa 15 anti-patrones con impactos técnicos detallados
- Certificación OCEB 2 (5 niveles, ramas negocio/técnica)
- Frameworks SEQUAL y GoM (calidad modelos)
- Casos de uso y mejores prácticas por industria

---

## Checklist Rápido — Antes de Exportar Proceso

```
CORRECCIÓN (Peso 3/3)
[ ] Sin deadlocks, bucles infinitos, trampas sincronización
[ ] Sin nodos desconectados o flujos huérfanos
[ ] Tipos tarea acordes realidad técnica
[ ] Sin redundancia lógica
[ ] Gateways simétricos (split/join pares)

COMPLETITUD (Peso 3/3)
[ ] Todos elementos requerimiento representados
[ ] Evento inicio + evento fin explícitos
[ ] Todos resultados gateways decision modelados (sí/no)
[ ] Flujos excepción vía Boundary Events

CLARIDAD (Peso 2-3/3)
[ ] Etiquetas correctas (Verbo-Objeto)
[ ] Cero elementos sin etiquetar
[ ] Espaciado visual limpio
[ ] Cruces flujos minimizados
[ ] Condiciones XOR rotuladas

ANTI-PATRONES (0/15 esperado)
[ ] Revisar lista 15 anti-patrones
[ ] Confirmar cero violaciones
[ ] Validar con herramienta automatizada

LISTO → Exportar a Motor BPM
```

---

## Próximos Pasos

1. **Selecciona nivel** (Descriptive/Analytic/Executable)
2. **Aplica 7PMG** en secuencia durante diseño
3. **Audita con 3C** — corrige desviaciones
4. **Valida anti-patrones** — 15 puntos
5. **Automatiza** con Trisotech/SpiffWorkflow
6. **Documenta** supuestos y limitaciones

---

Estándar OMG ISO/IEC 19510 — Método y Estilo Bruce Silver — Investigaciones 7PMG — Taxonomía Rozman
