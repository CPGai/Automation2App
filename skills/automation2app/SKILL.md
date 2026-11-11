---
name: automation2app
description: Prepare, integrate, and validate converting an automation or CLI into a user-facing local web application, optionally with conversational assistance. Use when explicitly requested, when a project adopts Automation2App, or when converting an existing automation. Do not impose it on unrelated websites, isolated visual fixes, internal-only scripts, or visual guides.
---

# Automation2App

Preparar y dirigir la conversión de automatizaciones en aplicaciones operables por usuarios finales. Usar este skill como agente desarrollador; el asistente conversacional del producto es otro componente. Mantener el patrón local-first, CLI estructurada, Web UI y conversación incluida, diferida o excluida por decisión explícita.

## Seleccionar contexto y modo

1. Leer las instrucciones del proyecto, su especificación y tareas canónicas. Identificar intención, capacidad, fase, alcance y autorizaciones vigentes; separar hechos de supuestos.
2. Seleccionar una fila. No ejecutar modos sucesivos por haber invocado el skill.

| Situación | Modo / salida |
| --- | --- |
| Intención insuficiente | Aclarar con interview-me o idea-refine, si están disponibles |
| Falta especificación aprobada | Preparación/especificación: definir conversión y presentar para aprobación; detenerse antes de plan y tareas |
| Especificación aprobada, falta plan | Preparación/planeación: proponer dependencias y tareas; conservar la aprobación previa a implementación |
| Integración solicitada, tarea aprobada y capacidad preparada | Integración: conectar solo la capacidad autorizada |
| Solicitud de revisar integración existente | Validación: evidencia por criterio, hallazgos y estado |

3. Leer [la integración con Agent Skills](references/agent-skills-integration.md) para la fase seleccionada. Resolver skills por nombre y capacidades reales; no asumir slash commands ni rutas de caché. No reiniciar using-agent-skills en bucle.
4. Si falta un skill o una herramienta, declarar la limitación y proponer el proceso equivalente. No fingir ejecución ni instalar herramientas sin autorización.
5. Para portar el paquete o valorar otro anfitrión, leer [la guía de adaptación](references/harness-adaptation.md). No usarla para atribuir compatibilidad ya comprobada.

## Preparación

- Definir usuario, recorrido, capacidades con ID estable, modalidades y criterios de éxito. Registrar la conversación como incluida, diferida o excluida por decisión; no descartarla silenciosamente.
- Usar [la plantilla de adopción](assets/project-adoption.md) dentro de la especificación existente; no crear una segunda especificación si existe un formato canónico.
- Leer [el contrato operativo](references/operation-contract.md) al definir operaciones, permisos, CLI o conversación. No seleccionar proveedor, autenticación o framework web por defecto.
- En especificación, presentar la propuesta y detenerse antes de planear o implementar. Tras aprobación, aportar al plan y tracker existentes dependencias de preparación, integración y verificación.
- Inspeccionar el contenido de tasks/plan.md y tasks/todo.md o su equivalente antes de escribir. Actualizar el mismo trabajo; si es otro alcance con pendientes, presentar el conflicto sin sobrescribir, renombrar ni mover archivos.
- Añadir la regla breve de adopción al archivo de reglas del proyecto solo con adopción aprobada y autorización de ese cambio. No editar el plugin, su caché o un router global.

## Integración

Comprobar antes de conectar cada capacidad:

1. Alcance y tarea aprobados; usuario, modalidad y recorrido identificados.
2. Automatización validada con entradas, resultados, fallos y evidencia vigente.
3. Operaciones/CLI y resultados estructurados definidos.
4. Autorización, nivel de riesgo, destinos y precondiciones definidos.
5. Dependencias y entorno disponibles.
6. Aceptación del recorrido y método de verificación definidos.

Si falta una condición, registrar brecha, bloqueo y trabajo de preparación; no construir la integración ni reescribir el sistema para aparentar preparación.

Reutilizar operaciones comunes para CLI, web y chat. Mantener UI y asistente como consumidores del contrato; el backend confiable valida y autoriza. No conceder al LLM del producto terminal general ni registro libre de comandos. Esto no prohíbe las herramientas de desarrollo autorizadas del agente implementador.

Integrar un corte por capacidad con los skills pertinentes. No exigir terminar toda la automatización para integrar una capacidad lista. Cambios arquitectónicos, permisos o alcance nuevos requieren decisión HITL antes de actuar.

## Validación

- Vincular evidencia a versión/huellas, entorno y tarea. Verificar recorridos reales y resultados; una captura de pantalla no prueba ejecución.
- Comprobar permisos, confirmaciones, rechazos, errores y efectos inciertos según el contrato. No anunciar éxito basándose solo en texto del modelo.
- Distinguir evaluación documental del skill de pruebas ejecutadas del runtime. Prescribir un control no demuestra que un backend lo aplique.
- Registrar resultado por criterio y bloqueos. Si falla la IA, comprobar el funcionamiento previsto de CLI/web y declarar las limitaciones del perfil conversacional.
- Antes de retomar, comprobar cambios del código, contratos y datos relevantes; invalidar evidencia afectada. Usar Git si existe o versiones/huellas sin inventar un SHA.

## Autoridad y límites

Separar aprobación de desarrollo (especificación, plan, alcance, instalación y despliegue) de autorización del usuario final para operaciones de la aplicación. Ninguna reemplaza a la otra.

Conservar autorizaciones ya concedidas dentro de su alcance; no pedirlas otra vez por cambiar de modo. Una aprobación de especificación o plan no autoriza acciones consecuenciales ni relajar permisos.

No implementar durante preparación; no adoptar en otro proyecto, instalar globalmente, publicar, migrar, gestionar credenciales ni seleccionar nuevos proveedores/gastos sin autorización aplicable. No crear un nuevo backlog ni un segundo orquestador.

## Salida y continuidad

Actualizar alcance/contratos en la especificación; dependencias en el plan; estado en el tracker canónico; evidencia donde indique el proyecto. Registrar bloqueos y aprobación además del estado de capacidad: prevista → automatizada-validada → integrada → verificada. Ningún estado concede permisos.

Para trabajo documental, entregar propuesta y decisiones pendientes. Para una ejecución material, entregar Result, State, Changes, Files, Verification, Failures, Deviations, Assumptions, Decisions Required y Provenance, usando “no aplica” cuando corresponda. Identificar próxima tarea y puerta pendiente.
