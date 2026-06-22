# Ejemplos Prácticos — BPMN 2.0 en Acción

> **Casos reales de aplicación de metodología y anti-patrones**

---

## Caso 1: Proceso de Venta Online (Nivel Analytic)

### Escenario
Sistema e-commerce: Cliente coloca orden, sistema procesa pago, prepara envío, notifica estado.

### Diagrama ASCII (Estructura BPMN)

```
START EVENT ORDER RECEIVED
 ↓
 (Inicio)
 ↓
 [Validar Orden ] ← Tarea: Verbo-Objeto (G6)
 ↓
 [<> XOR Split] ← Gateway mínimo (G2)
 ↙ ↘
 [NO]  [SI]
 ↓ ↓
[Reject] [Process Payment]
 ↓ ↓
 │ [Timer: Timeout 24h] ← Boundary Event
 │ ↙ ↘
 │ [Continue] [Interrupt: Cancel Order]
 │ ↓ ↓
 │ [Prepare Shipment] [Refund]
 │ ↓ ↓
 │ [Notify Customer] │
 │ ↓ ↓
 └─→ [<> Merge] ← Split/Join Simétrico (G4)
 ↓
 (Fin: Order Completed)

VALIDACIÓN 7PMG:
 G1: 8 elementos (< 30)
 G2: Gateways simples 
 G3: 1 inicio + 1 fin 
 G4: XOR split/join simétricos 
 G5: Solo XOR + AND (no OR)
 G6: "Validar Orden", "Procesar Pago" (Verbo-Objeto) 
 G7: Descomposición no necesaria 
```

### Validación Marco 3C

| Dimensión | Cumple | Observación |
|-----------|--------|-------------|
| **Corrección** | SI | Sin deadlocks, split/join simétricos, tipos tarea definidos |
| **Completitud** | SI | Todos elementos: validación, pago, rechazo, envío, notificación |
| **Claridad** | SI | Etiquetas Verbo-Objeto, sin cruce flujos, timeout visible |

### Anti-patrones Evitados
```
 AP#1: Elementos desconectados → Todos conectados secuencialmente
 AP#5: Flujo entre pools → Usar message flows si múltiples actors
 AP#9: Múltiples inicios → Solo 1 evento inicio
 AP#15: Excepción sin manejador → Boundary timeout tiene escape
```

---

## Caso 2: Autorización Médica (Nivel Descriptive - Mal Diseño → Corrección)

### INCORRECTO (Anti-patrones)

```
START
 ↓
[Task: Solicitud] ← AP#13: Tarea genérica, sin tipo
 ↓
[Gateway] ← AP#6: ¿Dónde genera decisión?
 ├─ → [Task: Revisar]
 │
 └─ → [Task: Análisis] ← Ambiguo: dos rutas sin condición clara
 ↓
[Task] ← AP#8: Sin etiqueta + sin salida = COLGADA

 [END] ← AP#3: Fin mal conectado (no todos flujos llegan)
```

**Problemas Detectados**
```
AP#1: Elemento "Análisis" sin conexión a fin
AP#6: Gateway sin tareas mensajería
AP#8: Elemento colgado sin salida
AP#9: Ambigüedad decisión
AP#13: Tareas genéricas sin tipo
```

### CORRECTO (Aplicando 7PMG)

```
(Inicio: Solicitud Recibida)
 ↓
 [Validar Documentación] ← G6: Verbo-Objeto
 ↓
 [<> XOR: Documentos OK?] ← G2: Gateway simple
 ↙ ↘
 [NO] [SÍ]
 ↓ ↓
[Solicitar [Revisar Médico]
 Documentos] ↓
 ↓ [Aprobar/Rechazar]
 │ ↓
 └─→ [<> Merge] ← G4: Simétrico XOR split/join
 ↓
 [Notificar Paciente] ← G6: Verbo-Objeto
 ↓
 (Fin: Autorización Completada)

VALIDACIÓN 7PMG: Todo OK 
```

**Mejoras Aplicadas**
```
 G6: Etiquetas Verbo-Objeto claras
 G4: Simetría split/join
 G3: Único inicio + fin
 Sin anti-patrones
 Claridad 3C: Diagrama autodescriptivo
```

---

## Caso 3: Fabricación (Nivel Executable + Boundary Events)

### Escenario
Planta de producción: recibe orden, programa máquina, inicia producción con timeouts y recuperación de fallos.

```
(START: New Production Order)
 ↓
[Schedule Machine]
 ↓
[Start Production] ← Con 3 Boundary Events
 │
 ├─→ [Error: Equipment Failure] (Interruptor: ())
 │ ↓
 │ [Emergency Stop]
 │ ↓
 │ [Notify Maintenance]
 │ ↓
 │ (Fin: Production Failed)
 │
 ├─→ [Timer: Quality Check Needed] (No-Interruptor: ()···)
 │ ↓ (paralel)
 │ [Interrupt Quality Test] (no detiene producción)
 │ ↓
 │ [Send: Enviar alerta QA]
 │
 └─→ [Timer: Timeout 8h] (Interruptor)
 ↓
 [Rollback Production]
 ↓
 (Fin: Timeout)

 [Flujo Normal]
 ↓
 [<> XOR: Quality OK?]
 ↙ ↘
 [NO] [SÍ]
 ↓ ↓
[Retry] [Package & Label]
 ↓ ↓
 └─→ [<> Merge]
 ↓
 [Ship Order]
 ↓
 (Fin: Completed)
```

### Boundary Events (Tabla)

| Event | Tipo | Trigger | Acción | Impacto |
|-------|------|---------|--------|---------|
| Equipment Failure | Interruptor | Error sensor | Stop + Maintenance | Interrumpe producción |
| Quality Check | No-Interruptor | Timer | Aviso paralelo | Monitoreo sin interrumpir |
| Timeout 8h | Interruptor | Duration | Rollback | Cancela si se excede |

### Variables de Datos (Executable Level)

```xml
<itemDefinition id="OrderType">
 <itemComponent name="orderId" type="string"/>
 <itemComponent name="productId" type="string"/>
 <itemComponent name="quantity" type="integer"/>
 <itemComponent name="startTime" type="dateTime"/>
</itemDefinition>

<!-- En tareas: mapeo variables -->
<serviceTask id="scheduleTask">
 <ioSpecification>
 <dataInput name="machineId" type="string"/>
 <dataInput name="duration" type="duration"/>
 </ioSpecification>
</serviceTask>
```

### Validación 3C

```
 CORRECCIÓN: Boundary events bien conectados, sin deadlocks
 COMPLETITUD: Rutas normal + excepciones + timeout mapeadas
 CLARIDAD: 3 Boundary Events claramente diferenciados
```

---

## Galería de Anti-patrones (Lo que NUNCA hacer)

### Anti-patrón #1: Actividades Desconectadas

```
 MALO:
 [Task A] ← No conecta a nada
 
 (Inicio)
 ↓
 [Task B] → [Task C] → (Fin)

PROBLEMA: Task A nunca se ejecuta (no alcanzable)
SOLUCIÓN: Conectar Task A en flujo secuencial

 BUENO:
 (Inicio)
 ↓
 [Task A] → [Task B] → [Task C] → (Fin)
```

### Anti-patrón #5: Flujo Directo Entre Pools

```
 MALO:
 Pool 1 Pool 2
 [Task A] ═══════╳═══ [Task B]
 
 Flujo secuencia CRUZANDO pools (PROHIBID)

 BUENO:
 Pool 1 Pool 2
 [Task A] ─────m──→ [Receive B]
 (message flow)
 
 Solo flujos MENSAJE entre pools
```

### Anti-patrón #6: Gateway Ejecutando Mensaje

```
 MALO:
 [Task] → [XOR Gateway] ──Send Message──→ [External]
 (gateway NO puede enviar)

 BUENO:
 [Task] → [Send Task] ──Message Flow──→ [External]
 ↓
 [XOR Gateway]
```

### Anti-patrón #13: Tarea Genérica en Executable

```
 MALO (Level 3 Executable):
 <task id="task1">
 <name>Procesar</name>
 <!-- Sin especificar tipo -->
 </task>

Motor no sabe: ¿Humano? ¿Sistema? ¿Script?

 BUENO:
 <serviceTask id="task1">
 <name>Procesar con Sistema</name>
 </serviceTask>
 
 <userTask id="task2">
 <name>Revisar Manualmente</name>
 </userTask>
 
 <scriptTask id="task3">
 <name>Calcular Impuestos</name>
 <script>JavaScript code</script>
 </scriptTask>
```

---

## Ejemplo Completo: Crédito Bancario (3 Niveles)

### NIVEL 1: Descriptive

```
(Solicitud Recibida)
 ↓
 [Evaluar Crédito]
 ↓
 [<> Aprobado?]
 ↙ ↘
 [NO] [SÍ]
 ↓ ↓
[Rechazar] [Desembolsar]
 ↓ ↓
 └─→ (Fin)

Enfoque: Stakeholders ejecutivos
Elementos: 6 (simple, sin detalles)
Excepciones: Ninguna
```

### NIVEL 2: Analytic

```
(START: New Credit Application)
 ↓
[Register Application] (entrada datos)
 ↓
[Validate Documentation] (checar completitud)
 ↙ ↘
 [OK] [Missing]
 ↓ ↓
 │ [Request Documents]
 │ ↓
 │ [Timer: Timeout 5 days] ← Boundary No-Interrupt
 │ ↓
 │ [Message: Reminder sent]
 │ ↓
 └─→ [<> XOR: All docs?]
 ↙ ↘
 [NO] [SÍ]
 ↓ ↓
 [Reject] [Analyze Credit Score]
 ↓ ↓
 │ [<> Score > 650?]
 │ ↙ ↘
 │ [NO] [SÍ]
 │ ↓ ↓
 │ [Review] [Check Income]
 │ ↓ ↓
 │ │ [Calculate Risk]
 │ │ ↓
 │ │ [<> Risk OK?]
 │ │ ↙ ↘
 │ │ [NO] [SÍ]
 │ │ ↓ ↓
 │ │ [Reject] [Approve]
 │ │ ↓ ↓
 └───→ [<> Merge]
 ↓
 [Notify Customer]
 ↓
 (Fin: Process Completed)

Enfoque: Analistas, optimización
Elementos: 18 (completo, con flujos)
Excepciones: 1 timeout para documentos
KPIs: Ciclo tiempo, tasa aprobación, % rechazados
```

### NIVEL 3: Executable

```xml
<process id="creditProcess">
 <!-- VARIABLES -->
 <itemDefinition id="ApplicationData">
 <itemComponent name="applicantId" type="string"/>
 <itemComponent name="creditScore" type="integer"/>
 <itemComponent name="monthlyIncome" type="decimal"/>
 <itemComponent name="riskRating" type="string"/>
 <itemComponent name="approvalStatus" type="string"/>
 </itemDefinition>

 <!-- EVENTOS -->
 <startEvent id="startEvent">
 <name>Application Received</name>
 </startEvent>

 <!-- TAREAS SERVICE (integración sistema) -->
 <serviceTask id="registerTask">
 <name>Register Application</name>
 <ioSpecification>
 <dataOutput name="applicationId"/>
 </ioSpecification>
 <extensionElements>
 <property name="url" value="http://api.bank.com/applications"/>
 <property name="method" value="POST"/>
 </extensionElements>
 </serviceTask>

 <!-- TAREAS USER (formulario interactiv) -->
 <userTask id="reviewTask">
 <name>Manual Review by Analyst</name>
 <ioSpecification>
 <dataInput name="applicationData"/>
 <dataOutput name="reviewNotes"/>
 </ioSpecification>
 </userTask>

 <!-- BUSINESS RULE TASK (invocar DMN) -->
 <businessRuleTask id="calculateRiskTask">
 <name>Calculate Risk Rating</name>
 <decisionRef="riskCalculationDecision"/>
 </businessRuleTask>

 <!-- GATEWAYS exclusivos con condiciones -->
 <exclusiveGateway id="scoreGateway">
 <name>Credit Score Check</name>
 </exclusiveGateway>

 <sequenceFlow sourceRef="scoreGateway" targetRef="approvePath">
 <conditionExpression>creditScore >= 650</conditionExpression>
 </sequenceFlow>

 <!-- BOUNDARY EVENTS: Timeouts + Escalaciones -->
 <boundaryEvent id="docTimeout" attachedToRef="getDocumentsTask" cancelActivity="false">
 <timerEventDefinition>
 <timeDuration>P5D</timeDuration> <!-- ISO 8601: 5 días -->
 </timerEventDefinition>
 </boundaryEvent>

 <sequenceFlow sourceRef="docTimeout" targetRef="sendReminder"/>

 <!-- SEND TASK: Notificación -->
 <sendTask id="notifyTask">
 <name>Send Approval Email</name>
 <outgoing>notifyFlow</outgoing>
 </sendTask>

 <!-- END EVENT -->
 <endEvent id="endEvent">
 <name>Process Completed</name>
 </endEvent>
</process>

<!-- DMN Decisión (integrada) -->
<decision id="riskCalculationDecision">
 <decisionTable>
 <inputClause>
 <inputExpression>creditScore</inputExpression>
 </inputClause>
 <outputClause>
 <outputExpression>riskRating</outputExpression>
 </outputClause>
 <rule>
 <condition>[ < 600 ]</condition>
 <conclusion>HIGH</conclusion>
 </rule>
 <rule>
 <condition>[ >= 600, < 700 ]</condition>
 <conclusion>MEDIUM</conclusion>
 </rule>
 <rule>
 <condition>[ >= 700 ]</condition>
 <conclusion>LOW</conclusion>
 </rule>
 </decisionTable>
</decision>
```

### Comparación 3 Niveles

| Aspecto | Descriptive | Analytic | Executable |
|---------|-------------|----------|------------|
| Audiencia | Ejecutivos | Analistas | Desarrolladores |
| Elementos | 6 | 18 | 25+ (con extensiones XML) |
| Excepciones | 0 | 1 timeout | Múltiples (timeouts, errors, compensations) |
| Detalle Tareas | Abstractas | Especificadas | Tipificadas + parámetros |
| KPIs | Estratégicos | Operativos | Métricas técnicas |
| Generador | Observador | Analista | Desarrollador |
| Validable | Alineación | Simulación | Motor BPM |

---

## Checklist de Implementación BPMN

### Fase 1: Diseño (Nivel 1-2)

```
ANTES DE MODELAR:
□ Definir stakeholders y audiencia objetivo
□ Identificar casos de uso críticos (happy path + excepciones)
□ Mapear actores y sistemas involucrados
□ Definir KPIs esperados

DURANTE MODELADO:
□ Aplicar 7PMG en orden (G1-G7)
□ Validar contra 15 anti-patrones
□ Revisar 3C (Corrección, Completitud, Claridad)
□ Usar herramienta validación (Trisotech, Camunda)

REVISIÓN TÉCNICA:
□ ¿Todos elementos tienen etiqueta Verbo-Objeto?
□ ¿Gateways son simétricos (split/join)?
□ ¿Excepciones tienen Boundary Events?
□ ¿Modelo < 30 elementos? (si no, descomponer)

APROBACIÓN:
□ Stakeholders dan OK
□ Analista QA valida completitud
□ Score 3C ≥ 75
```

### Fase 2: Desarrollo (Nivel 3)

```
PREPARACIÓN CÓDIGO:
□ Especificar tipos tarea (Service/User/Script/Business Rule)
□ Mapear variables entrada/salida (data mappings)
□ Configurar integraciones (APIs, bases datos)
□ Definir scripts/reglas de negocio

VALIDACIÓN TÉCNICA:
□ Soundness check (SpiffWorkflow)
□ XML serialización válida
□ Expresiones lógicas compilables
□ Variables mapeadas correctamente

TESTING:
□ Happy path manual
□ Excepciones simuladas
□ Load testing (throughput, concurrency)
□ Monitoring setup (métricas, alertas)

PRODUCCIÓN:
□ Despliegue motor BPM
□ Configuración observabilidad
□ Runbook escalación
□ Plan rollback
```

---

## Casos por Industria

### Healthcare: Admisión Paciente
```
Nivel 1: Recibir → Triagear → Consulta → Alta
Nivel 2: + Validar seguros, + Excepciones COVID/urgencia
Nivel 3: + Service tasks (EMR system), + Business rules (protocolos médicos)
```

### Finanzas: Transferencia Dinero
```
Nivel 1: Solicitud → Validar → Transferir
Nivel 2: + Detección fraude, + Límites, + Auditoría
Nivel 3: + APIs banco, + Compensaciones transaccionales, + Reintentos
```

### Logística: Envío Paquete
```
Nivel 1: Recibir → Empacar → Enviar
Nivel 2: + Inventario, + Rutas optimización, + Excepciones entrega
Nivel 3: + WMS API, + Tracking real-time, + Escaladas automáticas
```

---
