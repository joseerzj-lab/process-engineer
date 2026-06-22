# process-engineer: BPMN 2.0

Metodología científica para diseño, validación y optimización de procesos con BPMN 2.0.
Estándar OMG | ISO/IEC 19510 | Especificación 2.0.2

## Archivos

```
SKILL.md      <- guía ejecutiva accionable (empieza aquí)
REFERENCE.md  <- fundamentos científicos: historia, 7PMG detallado, 3C, anti-patrones
EXAMPLES.md   <- casos prácticos por nivel, galería anti-patrones, XML Executable
```

## Por rol

**Gestor/Ejecutivo** → SKILL.md § Nivel 1: Descriptive  
**Analista/Calidad** → SKILL.md § 7PMG + Marco 3C + Taxonomía anti-patrones  
**Desarrollador/BPM** → SKILL.md § Nivel 3: Executable + EXAMPLES.md § Caso 3

## Resolver problema específico

| Problema | Ir a |
|---|---|
| Diagrama tiene deadlock | REFERENCE.md § Anti-patrón #4 |
| ¿OR gateway o no? | SKILL.md § G5 |
| ¿Call Activity o Subproceso? | SKILL.md § Diferencia Crítica |
| Auditar calidad diagrama | SKILL.md § Checklist 3C |
| Ver anti-patrón con ejemplo | EXAMPLES.md § Galería |

## Herramientas

- **Trisotech / Cameo** — validación Método y Estilo en tiempo diseño
- **SpiffWorkflow** — soundness checks pre-producción
- **Camunda / Flowable** — motor ejecución BPMN 2.0

## Referencias

- OMG: https://www.omg.org/bpmn/
- Especificación: https://www.bpmn.org/
- Camunda docs: https://camunda.com/bpmn/
