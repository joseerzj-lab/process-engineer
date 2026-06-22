# Referencia Completa — BPMN 2.0 Ingeniería de Procesos

> **Documentación científica, histórica y metodológica**

---

## Fundamentos Estructurales y Evolución BPMN 2.0

### Historia del Estándar

**BPMN 2.0.2** (actual especificación oficializada por OMG y ratificada bajo **ISO/IEC 19510**) se consolida como estándar indiscutible para diseño, control, optimización y ejecución de procesos operativos.

#### Línea de Tiempo
```
2004 → Business Process Management Initiative (BPMI) — propone estándar
2005 → BPMI se fusiona con OMG — consolidación bajo consorcio único
2011 → BPMN 2.0 official release — semánticas ejecución matemáticas
2013 → BPMN 2.0.2 — ratificación ISO/IEC 19510
2024+ → Especificación vigente con extensiones ejecutables nativas
```

### Transformación Conceptual: BPEL → BPMN 2.0

**Problema Histórico (BPEL Era)**
- WS-BPEL (Web Services Business Process Execution Language) obligaba traducción XML intermedia
- Restricciones topológicas severas — no soportaba constructos complejos (ej: subprocesos ad-hoc)
- Dependencia de traductores terceros

**Solución (BPMN 2.0)**
- Formaliza **semánticas ejecución propias** con serialización XML nativa
- Diagrama gráfico = programa visual ejecutable simultáneamente
- Motores BPM interpretan directamente comportamiento gráfico
- Eliminación de dependencias traductores intermedios

### La Triple Corona OMG — Ecosistema Integrado

```
┌─────────────────────────────────────────────────┐
│ TRIPLE CORONA OMG │
├─────────────────────────────────────────────────┤
│ │
│ BPMN (Orquestación) ←→ CMMN (Gestión Casos) │
│ ↓ ↓ │
│ Flujos estructurados Actividades variable │
│ Secuencias predecibles Toma decisión humana │
│ Ad-hoc workflows │
│ │
│ ↓→← DMN (Decisiones) ←→↓ │
│ Reglas negocio operacionales │
│ Lógica condicional centralizada │
│ │
└─────────────────────────────────────────────────┘
```

### BPMN vs UML — Complementariedad

| Dimensión | BPMN | UML |
|-----------|------|-----|
| **Enfoque** | Orientado a procesos | Orientado a objetos |
| **Qué modela** | Secuencia actividades extremo-a-extremo | Arquitectura lógica aplicaciones |
| **Comunicación** | Entre participantes independientes | Dentro estructura código |
| **Tiempo** | Dinámico, casos instanciados | Estático, clases y objetos |
| **Casos de uso** | Flujos negocio, automatización | Diseño componentes software |
| **Integración** | Mapeo directo con UML (diagramas comportamiento) | Mapeo inverso desde BPMN |

### Certificación OCEB 2 (OMG Certified Expert in BPM)

Estructura de **5 niveles progresivos** divididos en dos ramas a partir nivel fundamental:

```
NIVEL 5 (Master Strategist)
 ↓
NIVEL 4 (Expert Practitioner)
 ↓
NIVEL 3 (Professional Developer)
 ↙ ↘
NIVEL 2 NIVEL 2
(Business) (Technical)
 ↙ ↘
 NIVEL 1 (Fundamental)
```

Cada nivel valida dominio creciente en estándar y metodologías gestión procesos.

---

## Niveles de Abstracción y Conformidad del Ciclo de Vida

### Tabla Comparativa Exhaustiva

#### **NIVEL DESCRIPTIVE (Nivel 1) — Visión Ejecutiva**

| Aspecto | Detalle |
|---------|---------|
| **Audiencia Principal** | Directores ejecutivos, gestores procesos estratégicos |
| **Propósito Central** | Definir alcance global, objetivos negocio, stakeholders |
| **Elementos Notación** | Subconjunto simplificado heredado diagramas flujo: <br>• Tareas abstractas (genéricas) <br>• Subprocesos simples (sin detalle interno) <br>• Piscinas y carriles organizativos <br>• Eventos inicio/fin básicos |
| **Flujos Excepción** | Omitidos completamente — solo camino estándar óptimo/alta probabilidad |
| **Indicadores KPI** | Conceptuales negocio: ciclos entrega macro, costos reclutamiento, tasas conversión, margen, ROIC |
| **Mapeo Procesos** | Alto nivel, sin detalles operativos |
| **Rol Ingeniero Procesos** | **Observador estratégico y analista inicial** — limita detalles técnicos para no saturar visualización negocio |
| **Herramientas Recomendadas** | PowerPoint, Visio básico, Lucidchart nivel intro |
| **Validación Esperada** | Alineación stakeholders, cobertura funcional macro |

#### **NIVEL ANALYTIC (Nivel 2) — Optimización Operativa**

| Aspecto | Detalle |
|---------|---------|
| **Audiencia Principal** | Analistas procesos, ingenieros calidad, especialistas operaciones |
| **Propósito Central** | Mejora continua, simulación dinámica, optimización operativa Lean Six Sigma |
| **Elementos Notación** | Paleta completa BPMN 2.0 estándar: <br>• Eventos intermedios (timer, message, signal) <br>• Pasarelas decisión (XOR, AND, OR exclusivo) <br>• Almacenes datos, objetos datos <br>• Eventos frontera (interrupts, non-interrupts) <br>• Subprocesos expandibles con detalle |
| **Flujos Excepción** | Mapeado riguroso de TODAS rutas alternativas, desvíos lógicos, usando Boundary Events e interrupciones |
| **Indicadores KPI** | Operativos detallados y parámetros simulación: <br>• Tiempos espera promedio/máximo <br>• Costos recursos por actividad <br>• Varianza ciclo proceso <br>• Tasas error/retrabajo <br>• Capacidad recursos (throughput) |
| **Mapeo Procesos** | Nivel de detalle operativo completo — permite simulación |
| **Rol Ingeniero Procesos** | **Puente conceptual** — traduce realidad operación física en modelo analítico coherente, simula impacto cambios operativos |
| **Herramientas Recomendadas** | Trisotech, ARIS, Signavio, Cameo Business Modeler, Bizagi |
| **Validación Esperada** | Simulación con datos reales, análisis sensibilidad, optimización indicadores |
| **Análisis Adicional** | Bottleneck identification, capacity planning, scenario testing |

#### **NIVEL EXECUTABLE (Nivel 3) — Automatización Producción**

| Aspecto | Detalle |
|---------|---------|
| **Audiencia Principal** | Desarrolladores software, integradores sistemas, equipos soporte BPM |
| **Propósito Central** | Despliegue automático en motor ejecución de procesos empresariales (BPMS) |
| **Elementos Notación** | Constructos técnicos avanzados: <br>• **Service Tasks** (invocar APIs REST/SOAP) <br>• **Script Tasks** (código ejecutable) <br>• **Business Rule Tasks** (invocar DMN) <br>• **Manual Tasks** (asignación humana) <br>• **User Tasks** (formularios interactivos) <br>• Variables sistema (data objects, correlation keys) <br>• Propiedades extensión técnica (timeouts, retry policies) |
| **Flujos Excepción** | Configuración precisa transacciones: <br>• Compensaciones datos (rollback) <br>• Reintentos conexión técnica con backoff <br>• Reversión transacciones empresariales <br>• Escaladas automáticas (escalation handlers) |
| **Indicadores KPI** | Codificados técnicamente en motor BPM: <br>• Puntos captura métricas (milestones) <br>• Variables contador (instancias completadas) <br>• Tiempo ejecución real (duration, wait time) <br>• Errores técnicos (exception logs) |
| **Integración Sistemas** | Mapeo variables XML, integración LDAP, conectores servicios datos externos (bases datos, APIs, message brokers) |
| **Rol Ingeniero Procesos** | **Desarrollador integraciones** — programa scripts, mapea variables, configura conexiones, gestiona errores técnicos |
| **Herramientas Recomendadas** | Camunda, Flowable, JBPM, Activiti, Apache ODE, SpiffWorkflow |
| **Validación Esperada** | Load testing, ejecución motor con datos reales, monitoreo producción, análisis logs |
| **Consideraciones Producción** | Transactionalidad, idempotencia, fault tolerance, monitoring, alerting |

### Simulación Industrial (SysCAD) — Principios Ingeniería

Para modelos con fines simulación en plataformas SysCAD, Aspen, MATLAB:

**Fase 1: Definición Alcance Rigurosa**
```
□ Alcance explícito del sistema
□ Límites físicos entrada/salida
□ Nivel detalle (macro vs micro)
□ Variables lógicas identificadas
→ PREVIENE desvío scope proyecto
```

**Fase 2: Validación Datos Operativos**
```
Fuentes confiables:
 Hojas técnicas equipamiento
 Análisis laboratorio (certificados)
 Setpoints historiales control
 Datos históricos operación (>=1 año)

PRINCIPIO GIGO (Garbage In, Garbage Out)
→ Calidad datos = Precisión matemática modelo
```

**Fase 3: Calibración Continua**
```
 NO: Modelos estáticos captura condición puntual
 SÍ: Calibración continua contra operación real
 Análisis sensibilidad variables límite
 Documentación transparente supuestos
 Logs cambios y versioning
```

---

## Directrices Empíricas 7PMG — Fundamentos Científicos

### Investigación Base

Mendling, Reijers y van der Aalst sintetizaron **hallazgos empíricos cuantitativos** que correlacionan:

```
Complejidad Topológica Diagrama
 ↓
 Propensión Error Cognitivo Modelador
 ↓
 Probabilidad Fallos Ejecución Física
 
CONCLUSIÓN: Existe correlación LINEAL DIRECTA
→ Modelos más complejos = más errores lógicos
```

### Marcos Complementarios de Calidad

**SEQUAL (Semiotic Quality Framework)** — John Krogstie
```
Evaluación modelos bajo 6 dimensiones comunicación:
1. Física → Representa aspectos físicos reales
2. Empírica → Adecuado interpretación usuarios
3. Sintáctica → Conforme especificación BPMN 2.0
4. Semántica → Significado acorde a intención
5. Pragmática → Comprensible auditor humano
6. Social → Aceptación y uso organización
```

**GoM (Guidelines of Modeling)** — Adaptación normas contables
```
Transferencia principios contabilidad a modelado conceptual:
• Claridad → Univocidad en interpretación
• Relevancia → Elementos aportan valor decisión
• Comparabilidad→ Modelos comparables temporalmente
• Eficiencia → Beneficio > costo mantenimiento
• Diseño Sist. → Estructura coherente jerárquica
```

### Las 7 Directrices Detalladas

#### **G1: Mínimos Elementos en Lienzo**

**Evidencia Científica**
```
Estudio: Mendling et al., 2007
Sample: 400+ procesos reales
Hallazgo: Correlación LINEAL y = 0.8x + 2
 (donde y = cantidad errores, x = cantidad elementos)
 
Interpretación: Cada elemento adicional incrementa 
 probabilidad error ~0.8x
```

**Implicación Operativa**
- Modelos < 15 elementos: ~15% tasa error
- Modelos 15-30 elementos: ~30% tasa error 
- Modelos > 30 elementos: ~50%+ tasa error

**Aplicación Práctica**
```
SI elemento NO aporta valor lógico CONTROL
→ ELIMINAR (mismo si redundancia con otra rama)

SI actividad es "paso trivial" (ej: "enviar confirmación")
→ COMBINAR con actividad precedente si posible
```

#### **G2: Minimizar Caminos Enrutamiento por Elemento**

**Concepto: Grado de Conectividad**
```
Elemento con ALTO grado conexidad = múltiples flujos entrada/salida
Riesgo: Análisis de sincronización exponencialmente complejo

Ejemplo MALO: Gateway recibe 5 flujos entrada, envía 4 salida
 Motor debe analizar 5×4=20 combinaciones
 
Ejemplo BUENO: Usar encadenamiento gateways
 G1 recibe 5, envía 1
 G2 recibe 1, envía 4
 Combinaciones: 5×1 + 1×4 = 9 (simplificado)
```

**Aplicación**
```
□ Enrutamiento implícito en tareas: PROHIBIDO
□ Usar pasarelas dedicadas split/join: OBLIGATORIO
→ Transparencia lógica control flujo
```

#### **G3: Exactamente 1 Evento Inicio + 1 Evento Fin**

**Estándar BPMN Permite**
```
Eventos inicio/fin son "opcionales" en ciertas configuraciones
(permite diseños con múltiples orígenes/destinos)
```

**Ingeniería de Procesos Exige**
```
Delimitador ÚNICO origen + conclusión para:
 Guiar lector claramente (pragmática)
 Análisis formal corrección estructural (lógica)
 Algoritmos validación Soundness (verificación estática)
 Determinismo en motor ejecución (técnico)
```

**Por Qué Falla Sin Esto**
```
 Procesos múltiples inicios
 → Ambigüedad: ¿qué dispara instancia?
 → Análisis formal falla (múltiples recorridos válidos)
 → Motor confundido (¿cuándo termina caso?)
```

#### **G4: Máxima Estructura (Split ↔ Join Simétricos)**

**Definición Modelo Estructurado**
```
Cada pasarela bifurcación (SPLIT) tiene:
• Correspondencia EXACTA y SIMÉTRICA
• Pasarela unión (JOIN) del MISMO TIPO lógico
• Encadenamiento en árbol equilibrado

Ejemplo ESTRUCTURADO:
 ├─ XOR-Split
 │ ├─ Task A
 │ └─ Task B
 └─ XOR-Join

Ejemplo DESESTRUCTURADO:
 ├─ AND-Split
 │ ├─ Task A ──→ XOR-Join X
 │ └─ Task B ──→ (sin join)
```

**Consecuencias del Mal Diseño**
```
Deadlock (Interbloqueo):
 Token entra AND-Join esperando N threads
 Pero solo N-1 threads arribar
 → Token BLOQUEADO PERMANENTEMENTE

Fragmentación Paralela:
 Múltiples threads independientes sin sincronización
 → Impredecible orden ejecución
 → Inconsistencia datos
```

#### **G5: Evitar Gateways Inclusivos (OR)**

**Problema Técnico**
```
Gateway OR (Inclusivo):

Decisión: "Procesar si Crédito OK?" [Sí/No]
 "Procesar si Edad OK?" [Sí/No]
 "Procesar si Ingresos OK?" [Sí/No]

Combinaciones válidas:
 0) Ninguno → Sync Point?
 1) Solo Crédito
 2) Solo Edad
 3) Solo Ingresos
 4) Crédito+Edad
 5) Crédito+Ingresos
 6) Edad+Ingresos
 7) Todos tres

Motor debe responder: "¿Sigue llegando thread?"
→ COMPLEJIDAD EXPONENCIAL sincronización asíncrona
```

**Solución Recomendada**
```
Reemplazar OR con composición XOR + AND:

AND-Split
 ├─ XOR (Crédito sí/no) ──→ Task A o Skip A ──→ AND-Join
 ├─ XOR (Edad sí/no) ──→ Task B o Skip B ──→ AND-Join
 └─ XOR (Ingresos) ──→ Task C o Skip C ──→ AND-Join

Resultado: Claridad pragmática + precisión técnica
```

#### **G6: Verbo-Objeto para Etiquetas Actividades**

**Estructura Obligatoria**
```
VERBO (acción infinitivo/imperativo) + OBJETO (sustantivo dominio)

 CORRECTO:
 • Validar Historial Crediticio
 • Procesar Orden Venta
 • Enviar Confirmación Pago
 • Registrar Cliente Nuevo

 INCORRECTO:
 • Proceso Facturas (sustantivo, ambiguo)
 • Orden (omite verbo)
 • Validación (sustantivo, no acción)
 • OK/Aceptado (adjetivo, sin objeto)
```

**Por Qué Importa**
```
Previene confusión:
 Acción ≠ Datos ≠ Eventos ≠ Área organizativa

Ejemplo:
 Etiqueta "Orden" ¿es?
 • La tarea de crear orden
 • El objeto de datos (orden)
 • El evento que dispara (nueva orden recibida)
 • El departamento (área de órdenes)
 
 Claridad → "Crear Orden" (actividad), "Orden" (dato)
```

#### **G7: Descomposición Jerárquica (>30 Elementos)**

**Evidencia Cognitiva**
```
George Miller, "The Magical Number Seven"
Capacidad memoria trabajo humana: 7±2 chunks

BPMN en práctica:
 Procesamiento visual modelos ~30 elementos máximo
 > 30 elementos → deterioro drástico comprensión

Estudio BPMN específico:
 30 elementos → 85% precisión lectura
 50 elementos → 45% precisión lectura
 
→ Degradación exponencial, NO lineal
```

**Estrategia de Descomposición**
```
Nivel 1: Proceso global (orquestación principal)
 ├─ Subproceso Colapsado A (representado como rectángulo +)
 ├─ Subproceso Colapsado B
 └─ Subproceso Colapsado C

Nivel 2: Expandir cada subproceso
 A.1, A.2, A.3, ... (< 30 elementos)
 
Nivel 3: Si algún A.X sigue siendo > 30
 → Descomponer recursivamente
```

---

## Patrones, Jerarquía y Gestión Excepciones

### Subproceso Embebido vs Call Activity (Profundidad)

#### **Subproceso Embebido**
```xml
<!-- Existe SOLO dentro contenedor proceso padre -->
<process id="parent">
 <subProcess id="embedded_sub">
 <startEvent id="start"/>
 <!-- lógica interna -->
 <endEvent id="end"/>
 </subProcess>
</process>
<!-- Si eliminas <process>, desaparece subproceso -->
```

**Características Técnicas**
```
Scope Variables: Comparte TODA variables padre (no aislamiento)
Serialización XML: Anidada dentro mismo archivo
Reusabilidad: No — solo en este proceso
Mantenimiento: Modificación en padre → cambio local solo
Uso Casos: Organización visual, lógica secuencial local
Gobierno: Descentralizado (cada proceso decide interno)
```

#### **Call Activity**
```xml
<!-- Invoca proceso DEFINIDO EXTERNAMENTE -->
<process id="parent">
 <callActivity id="call_sub" calledElement="shared_subprocess"/>
</process>

<!-- Proceso referenciado: puede estar en archivo distinto -->
<process id="shared_subprocess">
 <!-- Definición reutilizable -->
</process>
```

**Características Técnicas**
```
Scope Variables: MAPEO EXPLÍCITO entrada/salida (aislamiento estricto)
Serialización XML: Referencia externa por ID (calledElement)
Reusabilidad: Sí — invocable desde N procesos
Mantenimiento: Cambio en definición → propaga a TODAS invocaciones
Uso Casos: Subprocesos estándar corporativos, gobernanza
Gobierno: Centralizado (repositorio único)
Mapeo Datos: Variables entrada → in-mapping
 Variables salida → out-mapping
```

### Principios Bruce Silver: Método y Estilo

#### **Principio 1: Univocidad de Significado**
```
REGLA: Significado lógico debe ser COMPLETAMENTE COMPRENSIBLE
 del diagrama IMPRESO, sin consultar:
 • Documentación adjunta
 • Notas aclaratorias
 • Comentarios ocultos
 • Configuración en herramienta

IMPLEMENTACIÓN:
 Etiquetas claras Verbo-Objeto
 Todos elementos visualmente representados
 Lógica encapsulada jerárquicamente (subprocesos con nombre)
 Convenciones visuales consistentes (colores, símbolos)
```

#### **Principio 2: BPMN-I (Interoperabilidad)**
```
REGLA: Modelo debe tener ÚNICA SERIALIZACIÓN XML que garantice:
 • Visualización idéntica en herramientas distintas
 • Ejecución comportamiento idéntico
 • Sin distorsiones gráficas (posiciones elementos)
 • Sin cambios comportamiento técnico

RIESGO: Vendor lock-in por interpretaciones divergentes
SOLUCIÓN: Conformidad ESTRICTA especificación OMG 2.0.2
```

### Eventos de Frontera — Arquitectura Asíncrona

#### **Captura Asíncrona (Catching)**
```
Los Boundary Events operan en modo "catching":
• Esperan PASIVAMENTE un trigger específico
• NO generan el evento (son receptores)
• Cuando trigger ocurre → disparan acción

Triggers posibles:
 • Timer (timeout ISO 8601)
 • Message (recibir mensaje externo)
 • Signal (broadcast signal)
 • Error (excepción lanzada)
 • Escalation (escalada negocio)
 • Compensation (revierte transacción)
 • Custom/Conditional (expresión lógica)
```

#### **Interruptor vs No-Interruptor (Tabla Decisión)**

| Aspecto | Interruptor (O) | No-Interruptor (O)···· |
|---------|-------------|-------------------|
| **Trigger** | Al activarse | Al activarse |
| **Acción** | Cancela tarea INSTANTÁNEAMENTE | Clona token → ruta paralela |
| **Destrucción** | Destructiva inmediata | No destruye original |
| **Continuación Original** | Reemplazada por escape | Sigue normalmente |
| **Representación** | Trazo doble CONTINUO | Trazo doble DISCONTINUO |
| **Concurrencia** | No — secuencial escape | Sí — paralelo |
| **Caso Uso** | Timeout crítico (cancelar) | Alerta/Log (monitoreo) |
| **Ejemplo** | Si pago no llega en 24h → cancelar orden | Si pago demora > 4h → enviar recordatorio |

#### **Implementación Técnica**

**Interruptor: Flujo de Escape**
```
Task "Procesar Pago"
 ├─ [Normal: paymentReceived] → Task "Confirmar"
 └─ [Boundary Interruptor: timeout 24h] → Task "Cancelar Orden" → End

En ejecución:
 Si timeout dispara antes que pago llegue:
 • Token actual en "Procesar Pago" → ANULADO
 • Token nuevo → "Cancelar Orden" → fin
```

**No-Interruptor: Ruta Paralela**
```
Task "Procesar Pago"
 ├─ [Normal: completion] → Task "Confirmar" → End
 └─ [Boundary No-Interruptor: timer 4h] ──→ Task "Enviar Recordatorio" → (independiente)

En ejecución:
 Timer 4h dispara:
 • Token ORIGINAL sigue en "Procesar Pago"
 • Token NUEVO clonado → "Enviar Recordatorio"
 • Ambos avanzan en paralelo
```

---

## Marco 3C — Auditoría Exhaustiva

### Tabla de Criterios Ponderados

| Dimensión | Criterio Específico | Importancia | Peso | Implicación Técnica/Negocio si Viola |
|-----------|-------------------|-------------|------|-------|
| **Corrección** | Ausencia violaciones sintácticas (deadlocks, bucles ∞, trampas sincronización) | Alto | 3 | Modelo rechazado motor BPM → bloqueo operativo total |
| **Corrección** | Ausencia errores estructurales (nodos desconectados, flujos huérfanos) | Alto | 3 | Flujos no alcanzables → inconsistencia intercambio datos |
| **Corrección** | Ausencia violaciones semánticas (tipos tareas acordes realidad técnica) | Moderado | 2 | Malinterpretación funcionamiento → desarrollo diverge expectativa |
| **Corrección** | Evitar redundancia lógica (elementos sin valor control) | Moderado | 2 | Sobrecarga diseño → ruido visual, costo mantenimiento |
| **Corrección** | Simetría pasarelas (todo split tiene join correspondiente) | Bajo | 1 | Riesgo condiciones carrera, comportamientos impredecibles |
| **Completitud** | Representación todos elementos requerimiento | Alto | 3 | Omisión pasos críticos → desarrollo incompleto solución |
| **Completitud** | Inclusión eventos inicio/fin explícitos | Alto | 3 | Imposibilidad determinar origen/conclusión caso |
| **Completitud** | Modelado explícito resultados lógicos gateways | Moderado | 2 | Ramificaciones truncadas → tokens perdidos en rutas no modeladas |
| **Completitud** | Incorporación flujos gestión excepciones (Boundary Events) | Moderado | 2 | Vulnerabilidad operativa → sin planes mitigación fallos externos |
| **Claridad** | Ausencia etiquetas incorrectas | Alto | 3 | Confusión usuarios negocio → retrasos interpretaciones contradictorias |
| **Claridad** | Ausencia elementos sin etiquetar | Alto | 3 | Opacidad total → diagrama pierde valor autodescriptivo |
| **Claridad** | Ausencia problemas diagramación visual | Moderado | 2 | Fatiga visual → incremento tasa errores lectura manual |
| **Claridad** | Evitar cruces superposición flujos innecesaria | Moderado | 2 | Dificultad rastrear tokens especialmente en alta concurrencia |
| **Claridad** | Rotulación clara condiciones XOR-splits | Bajo | 1 | Dificultad discernir reglas toma decisiones |

### Scoring 3C

**Cálculo de Puntuación**
```
Score Corrección = Σ(Criterios Cumplidos × Peso) / Peso Total × 100
Score Completitud = Idem
Score Claridad = Idem

Score 3C Total = (Corrección × 0.4) + (Completitud × 0.35) + (Claridad × 0.25)

Categorías:
 ≥ 90: EXCELENTE (Listo producción)
 75-89: BUENO (Requiere ajustes menores)
 60-74: DEFICIENTE (Revisión significativa)
 < 60: INACEPTABLE (Rediseño requerido)
```

---

## Taxonomía: 15 Anti-patrones Rozman & Polančič (Completa)

> **Investigación empírica sobre desviaciones recurrentes por modeladores inexpertos**

### Tabla Exhaustiva con Soluciones

| ID | Anti-patrón | Categoría Lógica | Impacto Crítico | Solución Requerida | Prevención |
|----|-------------|-----------------|-----------------|-------------------|-----------|
| **1** | Actividades desconectadas en pool | Sintáctico + Pragmático | Partes proceso quedan estado no alcanzable; parálisis hilos ejecución | Enlazar obligatoriamente todos elementos pool con flujos secuencia continuos | Validador detecta nodos con indegree=0 (excepto eventos inicio) |
| **2** | Ausencia evento inicio | Pragmático | Incertidumbre sobre origen caso; áreas operativas no reconocen disparador | Incorporar obligatoriamente evento inicio CUALIFICADO que represente disparo orquestación | Motor BPM rechaza proceso sin start event en conformidad strict |
| **3** | Ausencia evento fin | Pragmático | Estancamiento casos activos en sistema; usuarios no saben cuándo culmina flujo | Modelar explícitamente eventos fin normales o terminación según corresponda | End event es requerido en conformidad nivel 2+ |
| **4** | Flujo cruzando límites subproceso | Sintáctico + Pragmático | Violación grave encapsulamiento jerárquico; colapso lógica interna ejecución | Garantizar flujo secuencial ingresa SOLO a través evento inicio subproceso | Herramienta debe validar que flujos externos no penetren subproceso internos |
| **5** | Flujo directo entre pools | Sintáctico | Error estructural crítico; flujos secuencia tienen PROHIBIDO atravesar contenedores independientes | Utilizar EXCLUSIVAMENTE flujos mensaje para comunicar interacciones entre pools | SpiffWorkflow/Camunda rechaza sequence flow crossing pool boundaries |
| **6** | Gateway ejecutando mensaje | Semántico | Gateways son SOLO enrutadores lógicos, no ejecutan tareas físicas ni procesamiento comunicaciones | Anteceder o suceder gateway con tareas específicas (Send/Receive Tasks) o eventos dedicados | Gateway debe tener incoming/outgoing sequence flows, no message flows |
| **7** | Evento frontera mal posicionado | Sintáctico | Error sintáctico; boundary events SOLO se asocian borde físico actividades operativas | Mover evento intermedio posicionarlo correctamente sobre borde actividad bound | Validador verifica attachedToRef apunta a actividad válida |
| **8** | Elemento "colgado" sin salida | Sintáctico | Tokens ejecución que alcancen nodo se desvanecen sin concluir caso éxito | Enlazar elemento sin salida continuación flujo secuencial o evento fin | Todas actividades excepto end events deben tener outgoing sequence flow |
| **9** | Múltiples eventos inicio redundantes | Pragmático | Sobrecarga cognitiva; usuarios asocian erróneamente que cada rol inicia flujo | Consolidar único evento inicio nivel orquestación; distribuir trabajo vía gateways decisión | Convención: máximo 1 start event por pool, 1 lane |
| **10** | Temporizador mal usado | Semántico | Retrasos operacionales severos o fallos ejecución síncrona en motor | Estudiar semántica temporizador (esperas relativas vs disparadores cíclicos ISO 8601) | Documenta duración ISO 8601 (P2DT3H = 2 días 3 horas) |
| **11** | Flujos imitando datos | Semántico | Ruido visual; confusión al equiparar secuencia lógica control con movimiento físico datos | Utilizar herramientas nativas BPMN (Data Objects, almacenes datos, asociaciones) | Data associations desacoplan control flow de data flow |
| **12** | Evento capturador como origen mensaje | Sintáctico | Incompatibilidad gramatical; flujos mensaje SOLO nacen elementos lanzadores o actividades | Configurar origen mensaje asociándolo a Send Task o evento lanzador calificado | Throwing events, activities generan; catching events, sequence flows reciben |
| **13** | Tareas genéricas en Executable | Semántico + Pragmático | Pérdida precisión; motor incapaz interpretar autom. tarea sin tipo definido | Calificar precisamente cada tarea (Manual, User, Service, Script, Business Rule) | XML serialization requiere taskType; motor rechaza tareas sin tipo |
| **14** | Start Timer posicionado secuencial | Sintáctico + Semántico | Timer intentará instanciarse autónomamente periódicamente vs actuar como espera secuencial | Reemplazar elemento por event intermedio capturador tiempo estándar | Start Timer es para instanciación periódica; intermediate timers para esperas |
| **15** | Flujo excepción desconectado | Semántico | Excepciones y fallas técnicas quedan huérfanas; imposibilita recuperación/reversión transaccional | Conectar rigurosamente salida cada Boundary Event interruptor → secuencia escape o tarea error | Todo interrupting boundary event debe tener outgoing sequence flow |

### Patrones de Detección (Herramientas)

```
Validación AUTOMATIZADA:

1. Nodos desconectados → graph connectivity analysis
2. Evento inicio/fin → node type inventory
3. Cruce pools → boundary detection
4. Gateway-Message confusion → node type + flow type check
5. Elementos colgados → outdegree inventory (excepto end events)
6. Redundancia elementos → duplicate task name detection
7. Data vs Control → flow type validation
8. Temporizador mal colocado → timer node position check
```

---

## Herramientas Validación Recomendadas

### **Trisotech BPMN Editor**
```
Capacidades:
 Preloaded Method & Style rules (Bruce Silver)
 Real-time violation highlighting
 Soundness analysis
 XML export con certificación conformidad
 Integración repositorio central

Detecta en Tiempo Diseño:
 • Service Tasks sin parámetro mapping
 • Decision gateways sin etiquetas condición
 • Procesos > 30 elementos (G7 warning)
 • Asimetría gateways
```

### **Cameo Business Modeler (MagicDraw)**
```
Capacidades:
 UML ↔ BPMN bidireccional
 Integración DMN y CMMN
 Validación customizable
 SysML para ingeniería sistemas

Validaciones:
 • Conformidad BPMN 2.0.2
 • Consistency checking
 • Traceability matrices
```

### **SpiffWorkflow**
```
Capacidades:
 Motor ejecución open-source
 Análisis estático soundness checks
 Validez expresiones lógicas XOR/AND
 Pre-deployment verification

Soundness Analysis:
 • Option to Complete: todo token puede alcanzar end
 • Proper Completion: token no se generan indefinidamente
 • No Dead Tasks: todas actividades alcanzables
```

### **Procesator / Bizagi**
```
Capacidades:
 Simulación con datos reales
 KPI tracking y optimization
 Colaboración temps-real
 Integración RPA
```

---

## Referencias Académicas Primarias

```
[1] Business Process Model and Notation - Wikipedia
[2] Decisioning — What is BPMN 2.0 Standard
[3] OMG BPMN Official Specification
[4] Orchestrating People and Systems with BPMN 2.0
[5] BPMN.org Specification Repository
[6] Mendling, J., Reijers, H. A., & van der Aalst, W. M. (2010). 
 "Seven Process Modeling Guidelines (7PMG)"
[7] Bizzdesign — BPMN Modeling Levels
[8] HEFLO Blog — BPMN Subprocesses Explained
[9] Rozman, T., Polančič, G., & Vajde Horvat, R. (2011).
 "Analysis of Common Process Modelling Mistakes in BPMN"
[10] Bruce Silver — BPMN Method and Style (2nd Edition)
[11] John Krogstie — SEQUAL Framework
[12] SysCAD — Seven Golden Rules of Process Modelling
[13] Flowable Documentation — BPMN 2.0 Constructs
[14] Red Hat Process Automation — BPMN Events
[15] Camunda — BPMN Execution Semantics
```

---

**Última actualización: 2026 | Estándar OMG ISO/IEC 19510:2013 | Conformidad BPMN 2.0.2**
