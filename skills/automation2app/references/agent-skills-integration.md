# Colaboración con Agent Skills

## Objetivo y marco

Automation2App es un proceso complementario al framework Agent Skills de Addy Osmani. Introducir preparación desde especificación; conservar la implementación de UI diferida hasta que la capacidad correspondiente esté validada. No modificar los skills originales para insertar una fase obligatoria global.

La base de diseño se examinó con Agent Skills 0.6.15. Es una referencia de integración, no una dependencia de una ruta o una garantía de compatibilidad con versiones posteriores. Comprobar la instalación real al adoptar.

## Elegir el proceso pertinente

| Etapa | Aporte de Automation2App | Skill de Agent Skills |
| --- | --- | --- |
| Aclarar | Usuario, objetivo y operación prevista | interview-me / idea-refine |
| Especificar | Adopción, modalidades, límites, criterios y contratos | spec-driven-development |
| Definir frontera | Operaciones tipadas y consumidores comunes | api-and-interface-design |
| Planear | Dependencias, tareas diferidas y evidencia de preparación | planning-and-task-breakdown |
| Construir | Corte aprobado por capacidad, pruebas relevantes | incremental-implementation / test-driven-development |
| UI | Recorrido, estados, accesibilidad y adaptación visual | frontend-ui-engineering |
| Seguridad | Autorización, entrada, puente local y secretos | security-and-hardening |
| Proveedores | Mecanismos admitidos y fuentes oficiales fechadas | source-driven-development |
| Navegador | Uso real, resultados y fallos | browser-testing-with-devtools o alternativa disponible declarada |
| Revisar/entregar | Revisión, paquete y lanzamiento autorizado | code-review-and-quality / shipping-and-launch |

Leer solo procesos pertinentes. Seguir las puertas aplicables de especificación y plan; no convertir esta tabla en una ejecución automática de todos los skills. Si un skill cambia de nombre o no existe, registrar la brecha y proponer equivalencia sin afirmar que fue invocado.

## Fuentes canónicas

| Información | Destino |
| --- | --- |
| Intención, contratos, modalidades, alcance y decisiones | Especificación del proyecto; respetar OpenSpec u otro sistema existente |
| Dependencias y diseño de ejecución | tasks/plan.md o convención declarada |
| Trabajo pendiente y estado | tasks/todo.md o tracker designado, uno solo |
| Adopción y enlace a la especificación | AGENTS.md o reglas equivalentes del anfitrión |
| Evidencia | Ubicación del proyecto, enlazada desde la tarea |

Inspeccionar antes de escribir. Nunca eliminar, sobrescribir o mover pendientes de otro alcance para hacer espacio. Si es el mismo trabajo, actualizar en su lugar conservando decisiones y progreso.

## Preparación en proyectos nuevos

1. Registrar intención y adopción propuesta en especificación; definir modalidades, operaciones y autorizaciones.
2. Presentar especificación. No producir tareas de implementación antes de su aprobación.
3. Con especificación aprobada, incluir preparación del contrato y conversión futura en el plan/tracker.
4. Definir la condición de inicio por capacidad y enlazar evidencia esperada.
5. Conservar aprobación del plan antes de implementación. Reutilizar aprobación explícita vigente si ya cubre el trabajo; no inferirla de la invocación del skill.

## Adopción en proyectos existentes

Inspeccionar comportamiento real, CLI, pruebas, permisos y pendientes. Mapear operaciones existentes antes de proponer cambios. Si una capacidad está lista y su tarea aprobada, integrar esa capacidad; si falta evidencia, registrar bloqueo. No exigir migración general ni reescritura.

Una adopción aprobada autoriza solo los cambios acordados. No modificar automáticamente otros proyectos o reglas globales.

## Retomar sin memoria de conversación

Identificar especificación/tarea, modo, autorización, estado y revisión de la evidencia. Comparar código/contratos relevantes con la revisión evaluada. Cambios que alteran el comportamiento invalidan su evidencia; mantener otras verificaciones solo si siguen siendo aplicables.

Si no se puede demostrar vigencia, registrar evidencia no confirmada y verificar antes de ejecutar integración. No reconstruir aprobaciones por conjetura. No inventar SHA si el proyecto carece de Git: usar versión y huellas de archivos pertinentes.

## Bloqueos y continuidad

Un bloqueo de proveedor no cancela silenciosamente conversación ni altera su alcance. Un bloqueo de contrato no se resuelve conectando la UI a comandos arbitrarios. Registrar bloqueo, próxima acción y quién debe decidir; mantener el trabajo ya validado.
