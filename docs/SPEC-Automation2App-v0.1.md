# Especificación: Automation2App

- Versión: 0.1
- Fecha: 11 de noviembre de 2026
- Estado: aprobada el 11 de noviembre de 2026; edición pública de la especificación original.
- Tipo: especificación del skill y de su integración con Agent Skills.
- Nombre propuesto del skill: `automation2app`.
- Base examinada: Agent Skills 0.6.15 instalado en este entorno.
- Alcance de esta especificación: diseño del skill documental. El estado posterior de instalación y validación se registra en VALIDATION.md; no autoriza despliegues de aplicaciones.

Nota editorial: las secciones que describen etapas futuras conservan el diseño de la versión original. La ejecución posterior se resume en [VALIDATION.md](VALIDATION.md). Se retiraron referencias privadas de transporte; no se modifican los contratos del producto.

## 1. Objetivo y usuario

Crear un skill reutilizable para que un agente desarrollador prepare, integre y valide la conversión de una automatización en una aplicación utilizable por personas sin conocimientos técnicos.

El skill acompaña el ciclo de Agent Skills: introduce requisitos desde especificación, aporta dependencias durante planeación y guía la integración cuando la capacidad automatizada correspondiente esté validada. No reemplaza el ciclo de desarrollo ni crea un segundo orquestador.

El usuario directo del skill es el agente desarrollador, con Carlos como autoridad de intención, arquitectura, alcance y aprobación. El usuario final opera la aplicación resultante mediante una Web UI y, cuando se incluya en el alcance aprobado, asistencia conversacional.

El chatbot de una aplicación es un componente del producto. No es el propio skill y no recibe por ello autoridad de desarrollo o una terminal general.

### Supuestos de diseño explícitos

- Se conserva el patrón local-first: lógica operativa accesible por CLI, presentación web local y asistencia conversacional con soporte y solicitud de acciones.
- La incorporación puede ser gradual por capacidad. No exige terminar toda la automatización ni construir toda la UI de una vez.
- El perfil conversacional puede quedar diferido, pero debe registrarse expresamente. No se elimina silenciosamente del alcance previsto.
- La entrega inicial del skill será documental: instrucciones, referencias y plantillas pequeñas. Un boilerplate ejecutable compartido será una decisión posterior.
- La instalación y su ubicación física se resolverán en la etapa correspondiente según el agente anfitrión; no se modificará la caché del plugin.
- No se seleccionan todavía framework web, proveedor de IA, modelo, almacenamiento o empaquetador.

## 2. Alcance y límites

### Incluido

1. Reglas de activación y selección de modo.
2. Contratos de entrada, salida, autorización y continuidad.
3. Integración con especificación, planeación, construcción y verificación de Agent Skills.
4. Criterios para pasar de automatización validada a integración por capacidad.
5. Patrón de operación común para CLI, web y chat.
6. Plantillas mínimas para adoptar el patrón en proyectos nuevos o existentes.
7. Escenarios verificables para evaluar el futuro skill.

### Fuera del alcance de esta versión

- Implementar una aplicación, un servidor, un chatbot, un dispatcher o una CLI concretos.
- Crear un framework alternativo, un router global, hooks de sesión o dependencias entre personas/agentes.
- Editar los skills originales, comandos o manifiestos del plugin Agent Skills.
- Instalar el skill, habilitarlo globalmente o añadir reglas a otros proyectos.
- Migrar datos, cambiar permisos, incorporar credenciales, publicar o desplegar servicios.
- Imponer una tecnología o distribuir un boilerplate como dependencia obligatoria.

## 3. Invariantes de arquitectura

| ID | Invariante |
| --- | --- |
| INV-01 | Automation2App aporta un proceso específico de conversión y reutiliza los procesos generales de Agent Skills. |
| INV-02 | Invocar el skill no autoriza avanzar de especificación a planeación, implementación o despliegue. Se conservan las aprobaciones aplicables. |
| INV-03 | Durante especificación y planeación se documenta la conversión; no se implementa la UI ni el runtime. |
| INV-04 | Una capacidad debe tener comportamiento automatizado validado antes de conectarla a una interfaz de ejecución para el usuario final. |
| INV-05 | CLI, web y chat reutilizan operaciones y reglas comunes. No duplican lógica de negocio ni permiten eludir permisos. |
| INV-06 | El modelo propone llamadas tipadas; el componente de ejecución confiable valida y autoriza. El modelo no decide sus permisos. |
| INV-07 | Ningún LLM obtiene una terminal general o puede registrar libremente nuevos comandos. |
| INV-08 | Existe un catálogo canónico de operaciones. Los esquemas CLI/chat y los consumidores web se derivan de ese contrato o se cotejan contra él. |
| INV-09 | El estado persistente reside en los artefactos del proyecto. No se depende de la memoria de una conversación. |
| INV-10 | Se preservan trabajo existente, restricciones y decisiones aprobadas. Cambios arquitectónicos o de alcance se escalan a HITL. |

## 4. Activación y exclusiones

### Activar cuando

- El usuario solicite Automation2App explícitamente.
- Un proyecto declare su adopción y esté especificando o planeando una automatización destinada a usuarios finales.
- Se solicite convertir scripts, una CLI o una automatización existente en una aplicación operable mediante web.
- Se solicite integrar o validar asistencia conversacional sobre operaciones de la aplicación.
- Se retome una fase Automation2App registrada en una especificación o tarea aprobada.

### No activar automáticamente cuando

- Se trabaje en una web sin relación con automatizaciones ni adopción declarada.
- Se corrija un detalle visual aislado sin afectar el contrato o la conversión.
- Se ejecute una automatización interna sin requisito de aplicación para usuarios finales.
- La solicitud trate exclusivamente de producir una guía visual de un producto ya existente.

En esos casos se usan los skills especializados que correspondan. No se añade Automation2App como requisito universal.

La descripción del futuro SKILL.md debe incluir estos disparadores. La activación por descripción ayuda al descubrimiento, pero no sustituye la referencia explícita del proyecto ni garantiza una secuencia automática.

## 5. Modos y contratos

Los modos son ramas de un solo skill. Cada invocación determina un modo y una fase; no ejecuta automáticamente todos los modos.

| Modo | Entradas mínimas | Trabajo | Salida | Condición de salida |
| --- | --- | --- | --- | --- |
| Preparación: especificación | Intención, usuarios, capacidades previstas y restricciones conocidas | Definir adopción, modalidades, límites, contrato operativo y criterios de conversión | Sección Automation2App en la especificación canónica, con decisiones pendientes | Presentar para aprobación y detenerse antes de planeación |
| Preparación: planeación | Especificación aprobada y estado del proyecto | Añadir tareas, dependencias y verificaciones con planning-and-task-breakdown | Aportes en tasks/plan.md y en la lista de tareas canónica | Presentar el plan y conservar su aprobación antes de implementar |
| Integración | Especificación y tareas aprobadas; capacidad automatizada validada | Comprobar preparación y conectar la siguiente capacidad autorizada | Cambio acotado, evidencia y estado actualizado | Verificación de la capacidad y handoff; continuar solo dentro de la autorización vigente |
| Validación | Capacidad integrada, criterios aprobados y entorno identificable | Verificar uso real, contrato, permisos y fallos | Evidencia de aceptación o hallazgos bloqueantes | Resultado por criterio; ninguna entrega se declara lista sin evidencia |

### Reglas de selección

- Intención insuficiente: usar interview-me o idea-refine para aclarar lo necesario.
- Falta especificación: preparación/especificación.
- Especificación aprobada, tareas pendientes de definir: preparación/planeación.
- Integración solicitada y requisitos satisfechos: integración.
- Revisión o aceptación de una integración existente: validación.
- Si se solicita integración sin preparación suficiente: informar la brecha y producir la especificación o el diagnóstico que corresponda, sin implementar.
- Si un skill requerido no está disponible: identificarlo y proponer un proceso equivalente; no fingir su ejecución ni instalar dependencias silenciosamente.
- Resolver skills por nombre y capacidades disponibles. No fijar rutas de caché con versiones.
- Leer y seguir un skill es una transferencia de proceso dentro del agente; no supone una API ejecutable ni un mecanismo universal de llamadas anidadas.

## 6. Integración con Agent Skills

| Etapa | Responsabilidad específica de Automation2App | Proceso reutilizado |
| --- | --- | --- |
| Definir | Usuario, recorrido, modalidades, adopción y criterio de éxito | spec-driven-development; interview-me si falta intención |
| Definir contratos | Operaciones, parámetros, resultados y límites entre componentes | api-and-interface-design |
| Planear | Dependencias, tareas diferidas, preparación y verificación | planning-and-task-breakdown |
| Construir | Integrar una capacidad aprobada por vez | incremental-implementation y test-driven-development |
| Construir UI | Recorridos, estados, accesibilidad y presentación | frontend-ui-engineering |
| Proteger | Validación confiable, autorización y secretos | security-and-hardening |
| Comprobar tecnologías | Validar mecanismos con documentación oficial | source-driven-development |
| Verificar | Comportamiento observable y recorridos en navegador | browser-testing-with-devtools o alternativa disponible declarada |
| Revisar y entregar | Revisión, evidencia, empaquetado y puesta en marcha autorizada | code-review-and-quality; shipping-and-launch cuando corresponda |

Se cargan solo los skills pertinentes a la tarea actual. Automation2App no vuelve a invocar using-agent-skills para reiniciar el ciclo ni instala un segundo router de sesión.

Las funciones del producto serán atendidas mediante tareas pequeñas y verificables. No se impone completar primero todo el backend y después toda la interfaz.

## 7. Persistencia y adopción por proyecto

### Fuentes canónicas

| Información                                         | Ubicación                                                                          |
| --------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Alcance, contratos y decisiones                     | Especificación canónica del proyecto; respetar OpenSpec u otro sistema ya adoptado |
| Diseño de ejecución y dependencias                  | tasks/plan.md, salvo convención explícita del proyecto                             |
| Tareas y estado                                     | tasks/todo.md o el tracker designado por el proyecto                               |
| Regla breve de adopción y ruta de la especificación | AGENTS.md o archivo de reglas equivalente                                          |
| Evidencia de verificación                           | Ubicación prevista por el proyecto, referenciada desde la tarea                    |

No crear un segundo backlog Automation2App. Antes de escribir planes o listas, inspeccionar si contienen trabajo pendiente. Actualizar el mismo trabajo en su lugar; si pertenecen a otro alcance, presentar el conflicto antes de reemplazarlos o moverlos.

### Campos mínimos de la sección Automation2App

- Adopción: propuesta o aprobada.
- Modalidades: visual, conversación de soporte y conversación con acciones; cada una incluida, diferida o excluida mediante decisión.
- Capacidades: identificadores estables, usuarios, entradas, salidas y operaciones correspondientes.
- Estado por capacidad: prevista, automatizada-validada, integrada o verificada.
- Criterio de preparación y referencias a evidencia.
- Política de autorización y operaciones de nivel crítico.
- Tareas relacionadas, dependencias y decisiones HITL pendientes.
- Entorno de ejecución previsto y limitaciones conocidas.

Los estados no otorgan autorización por sí mismos. Se registran también los bloqueos y las aprobaciones relevantes.

### Regla breve propuesta para proyectos adoptantes

> Este proyecto adopta automation2app según la sección correspondiente de su especificación canónica. Consultar ese skill al definir o planear capacidades destinadas a usuarios finales y al integrar o validar su interfaz. Durante preparación, documentar la conversión sin implementarla. Conservar las aprobaciones de Agent Skills y retomar el estado desde la especificación y las tareas existentes.

Esta regla solo se añade con adopción aprobada; no modifica otros proyectos ni copia el router completo.

### Continuidad

Al retomar: identificar tarea y modo; leer alcance y aprobación; revisar estado y evidencia; comprobar si el código o contrato relevante cambió. No reutilizar una validación invalidada por cambios. Usar commit y estado del árbol si existe Git; si no, registrar versiones o huellas de los archivos pertinentes y entorno sin inventar un SHA.

## 8. Patrón del producto resultante

La lógica de negocio constituye una capa reutilizable. La CLI proporciona acceso estructurado a las capacidades clave; la web y el chat consumen adaptadores que comparten operaciones, validación y autorización.

El dispatcher puede reutilizar la CLI mediante un proceso con argumentos separados o llamar a la misma capa de operaciones mediante una interfaz interna aprobada. Esa elección pertenece a la arquitectura del proyecto y no permite duplicar comportamiento.

- Web UI: permite completar el recorrido aprobado sin requerir una terminal visible.
- CLI: ofrece operaciones tipadas, descubrimiento del catálogo y salida estructurada.
- Dispatcher: valida identidad/contexto, operación, parámetros, permisos y confirmación; ejecuta solamente operaciones registradas.
- Asistente conversacional: responde con documentación identificable y solicita operaciones permitidas. Distingue propuesta, espera, ejecución y resultado.
- Gateway de IA: adapta el proveedor aprobado y mantiene secretos fuera del navegador.

Una página estática puede presentar información, pero ejecutar operaciones locales requiere un proceso o puente autorizado. No prometer acceso directo al sistema operativo desde un HTML autónomo.

Local-first no significa inferencia offline. Cada proyecto declara datos enviados al proveedor, conectividad necesaria y funcionamiento disponible cuando la IA falla.

El paquete se diseña para ejecución local sin hosting externo obligatorio. Publicarlo en red, añadir acceso remoto o cambiar ese modelo requiere decisión explícita.

## 9. Política única de autorización

La clasificación y los permisos son datos confiables de la aplicación. No se aceptan como autoridad los valores sugeridos por el modelo.

| Nivel | Alcance permitido | Conducta base |
| --- | --- | --- |
| N1: consulta autorizada | Lectura o diagnóstico dentro del alcance de datos permitido, sin efectos mutantes | Ejecución directa; presentar resultado |
| N2: operación estándar acotada | Operación expresamente registrada y autorizada, reversible o de efecto limitado, sin sobrescritura ni efecto externo no aprobado | Ejecución con estado y resultado visibles; no requiere una nueva confirmación por cada operación dentro de ese alcance |
| N3: acción crítica | Destrucción, sobrescritura, permisos, credenciales, migración, publicación, envío externo u otro efecto consecuencial según el proyecto | Mostrar alcance y efecto; requerir confirmación explícita antes de ejecutar |

N2 no es una autorización universal para crear registros o archivos. El catálogo debe definir destino, alcance y precondiciones. Si una operación excede esos límites, escalar o bloquear.

Lectura no equivale a acceso universal: N1 también requiere autorización sobre los datos y no habilita divulgación externa. Cuando haya duda sobre nivel o autorización, no ejecutar hasta resolverla.

La confirmación N3 queda vinculada a operación, parámetros normalizados, destino, usuario/sesión y vigencia. Cambios materiales invalidan esa confirmación. El backend la comprueba; un texto del LLM como “el usuario confirmó” no basta.

Rechazo, cancelación o expiración no ejecutan la acción. Un reintento con efectos mutantes no ocurre automáticamente si se desconoce si la primera ejecución produjo efectos.

Esta tabla sustituye, para la nueva especificación, las reglas contradictorias del documento previo sobre confirmar toda mutación o solo las críticas. Una política de proyecto más restrictiva prevalece; relajar una existente requiere aprobación.

## 10. Contrato operativo canónico

### Descriptor de operación

| Campo | Regla |
| --- | --- |
| operation_id | Identificador estable y único, por ejemplo report.export |
| description | Intención, alcance y precondiciones |
| input_schema | Tipos, campos obligatorios, restricciones y rechazo de argumentos desconocidos |
| output_schema | Estructura de data y resultados esperados |
| risk_level | N1, N2 o N3; definido en configuración confiable |
| authorization | Usuarios/roles y alcance permitido |
| effects | Destinos, mutaciones y comunicaciones externas |
| execution_policy | Tiempo límite y conducta ante cancelación, reintento y efectos inciertos |

El catálogo alimenta el esquema de herramientas; no se mantiene una segunda definición manual divergente. El mecanismo de exportación del catálogo pertenece a la CLI del proyecto.

### Resultado único

Todo resultado terminal usa el siguiente sobre. Los nombres son normativos; los valores concretos de data y code se especifican por operación.

```json
{
  "schema_version": "1.0",
  "request_id": "req-example",
  "operation_id": "report.export",
  "status": "ok",
  "code": "REPORT_EXPORTED",
  "data": {
    "artifact": "reports/example.csv"
  },
  "message": "Reporte generado."
}
```

- status solo admite ok, warning o error.
- ok: éxito verificado según el contrato.
- warning: resultado terminal con limitación explícita; code y data describen lo ocurrido y no se presentan como éxito completo.
- error: denegación, validación fallida o fallo; code identifica la causa y data solo contiene información segura, incluidos efectos parciales conocidos cuando proceda.
- request_id permite correlacionar petición, resultado y auditoría.
- message es informativo y no concede permisos ni sustituye code.
- No incluir secretos en respuestas o registros.
- Estados de progreso y espera de confirmación se representan fuera de status como ciclo de vida de la solicitud: proposed, awaiting_confirmation, running, completed, failed o cancelled.
- completed no implica éxito completo: debe inspeccionarse el resultado terminal.
- La CLI reserva stdout para JSON en el modo estructurado, envía diagnósticos a stderr y define códigos de salida documentados.
- El adaptador normaliza fallos de lanzamiento, timeout o salida inválida a error sin atribuir éxito al CLI.
- El chat solo confirma una acción realizada después de recibir evidencia válida del resultado.

### Controles de ejecución

Usar allowlist de operaciones y ejecutables; argumentos tipados y separados; validación de rutas y destinos; ejecución sin shell; límites y errores explícitos. Una lista de caracteres prohibidos no constituye la defensa principal contra inyección.

Proteger el puente local frente a solicitudes de otros orígenes y accesos no autorizados mediante controles adecuados al runtime elegido: enlace local, validación de origen/host y autorización de solicitudes, entre otros que requiera el proyecto. “Localhost” por sí solo no demuestra autorización.

## 11. Preparación para convertir una capacidad

La capacidad puede entrar a integración cuando exista evidencia de:

1. Alcance y tarea aprobados, con modalidad y usuario definidos.
2. Automatización funcional validada, con entradas, resultado y fallos conocidos.
3. Contrato CLI/operativo identificable y resultado estructurado acordado.
4. Nivel de autorización y precondiciones definidos.
5. Dependencias disponibles y entorno identificado.
6. Criterio de aceptación para el recorrido del usuario y verificación propuesta.

Si faltan condiciones, registrar el bloqueo y la tarea de preparación necesaria. No hacer una refactorización general ni declarar preparada la capacidad por disponer de una demo visual.

Para proyectos existentes se inspecciona primero el comportamiento real y se adopta incrementalmente. Si la adaptación exige cambiar arquitectura, esquemas o permisos, presentar la decisión antes de modificar.

## 12. Autenticación y proveedores de IA

El skill no promete reutilizar una suscripción de usuario ni supone que cualquier proveedor permita OAuth para una aplicación local.

Antes de implementar un adaptador se deben registrar: proveedor, mecanismo oficialmente admitido, autorización de uso aplicable, fuente oficial consultada y fecha, costos o límites relevantes y mecanismo de almacenamiento de secretos.

OAuth se considera cuando exista soporte documentado para ese cliente y uso. API key es otra alternativa sujeta a selección y validación; no se configura como fallback universal obligatorio.

Mantener tokens y claves en un almacén seguro apropiado al sistema. No incrustarlos en HTML/JS distribuido ni guardarlos en artefactos de especificación o telemetría.

Si no hay mecanismo compatible validado, bloquear el perfil conversacional afectado e informar la brecha. No cambiar de proveedor ni transmitir datos por una vía alternativa sin autorización.

## 13. Estructura prevista del futuro skill

| Recurso lógico | Propósito | Alcance inicial |
| --- | --- | --- |
| SKILL.md | Disparadores, selección de modo, procedimiento, límites y salida | Requerido |
| references/agent-skills-integration.md | Mapa de colaboración y reglas de continuidad | Requerido |
| references/operation-contract.md | Contratos, autorización y validaciones del patrón | Requerido |
| assets/project-adoption.md | Sección mínima de adopción y regla breve de proyecto | Requerido |
| agents/openai.yaml | Metadatos de interfaz si corresponden al anfitrión | Según instalación |

No crear scripts vacíos, un servidor de muestra ni un boilerplate en esta versión. Añadir recursos solamente si apoyan un procedimiento usado.

El SKILL.md debe ser conciso, cargar referencias según el modo y evitar copiar los procedimientos completos de Agent Skills. Los recursos son autocontenidos; no dependen de rutas relativas hacia la caché de otro plugin.

Los nombres de archivos son una propuesta de empaquetado, no carpetas creadas ni una lista de tareas de implementación.

## 14. Comandos, estilo y verificación futura

### Comandos

Esta entrega no introduce comandos ejecutables ni slash commands propios. Los del anfitrión solo se usan si están disponibles; mencionar un skill por nombre no demuestra que exista un comando equivalente.

Durante la futura implementación se descubrirán las rutas y comandos reales de inicialización y validación del entorno. Se anotarán comandos completos, resultados y versiones. No presentar rutas o comandos ilustrativos como pruebas realizadas.

Las aplicaciones adoptantes documentarán sus comandos reales de build, test, ejecución, exportación del catálogo y diagnóstico. Sus nombres no se fijan en esta especificación del skill.

### Estilo

Instrucciones directas, términos estables, pasos verificables y referencias de carga selectiva. Identificadores de operación únicos y parámetros explícitos. Diferenciar hechos observados, supuestos, recomendaciones y autorizaciones.

### Estrategia de evaluación

- Validación estructural del skill: frontmatter, nombres, referencias y metadatos.
- Evaluación de comportamiento: solicitudes realistas en contextos limpios que prueben modo, límites y resultados.
- Pruebas del contrato y autorización: en las aplicaciones que implementen el patrón.
- Verificación en navegador: recorridos reales y resultados observables; una captura aislada no prueba una operación.
- No declarar aprobación de escenarios todavía no ejecutados.

## 15. Criterios de aceptación y escenarios

| ID | Escenario | Resultado exigido |
| --- | --- | --- |
| AC-01 | “Planea esta automatización; tendrá Web UI después” sin especificación aprobada | Preparación/especificación; define conversión futura y se detiene antes de tareas e implementación |
| AC-02 | Misma solicitud con especificación aprobada | Preparación/planeación; registra dependencias y tareas en los artefactos canónicos; no construye UI |
| AC-03 | Automatización existente y tarea de integración aprobada | Diagnostica preparación y adapta una capacidad sin reescritura general |
| AC-04 | Solicitud de integrar una capacidad sin evidencia de automatización | Registra bloqueo; no declara preparada ni implementa la integración |
| AC-05 | Se retoma el trabajo en otra sesión | Reconstruye modo, tarea, autorización y evidencia desde archivos; detecta cambios relevantes |
| AC-06 | Existe un plan incompleto para otro alcance | No lo sobrescribe, renombra ni elimina; presenta el conflicto |
| AC-07 | Falta un skill especializado o un comando del anfitrión | Declara la limitación y propone alternativa; no simula disponibilidad |
| AC-08 | Proyecto visual sin automatización ni adopción | No impone Automation2App |
| AC-09 | Acción N3 confirmada y luego cambian sus parámetros | Invalida confirmación y bloquea ejecución hasta obtener una nueva válida |
| AC-10 | El modelo propone shell libre, comando desconocido o argumento inválido | El componente confiable rechaza la solicitud |
| AC-11 | El proveedor no tiene autenticación compatible validada | No promete acceso; bloquea integración conversacional afectada y conserva alcance pendiente |
| AC-12 | CLI falla, produce JSON inválido o no confirma efectos | UI/chat informan fallo o incertidumbre; no anuncian éxito ni reintentan mutaciones a ciegas |
| AC-13 | Una operación N2 intenta sobrescribir o exceder el destino autorizado | Se rechaza o escala según política; no se ejecuta con la autorización original |
| AC-14 | Se solicita adoptar el patrón en un proyecto | Se propone la referencia breve; no modifica la caché del plugin ni añade un router global |

AC-09 a AC-13 son requisitos que el skill debe trasladar a especificación, tareas y verificación del producto. Para evaluar el skill documental se comprueba que prescribe esas condiciones; para aceptar el runtime se requieren pruebas reales de la aplicación.

## 16. HITL, cambios y handoff

### Continuar dentro del alcance aprobado

Inspección, elaboración documental y, una vez autorizada la implementación, cambios acotados y reversibles previstos por las tareas. Resolver detalles mecánicos sin reabrir decisiones ya aprobadas.

### Solicitar decisión antes de actuar

Cambios de arquitectura o alcance, permisos, credenciales, datos sensibles, migraciones, destrucción, publicación, envío externo, nuevos proveedores o gastos no autorizados. Una aprobación de planeación no concede estas autorizaciones.

No inferir autorización de instalación de este skill por aprobar la arquitectura o esta especificación.

### Handoff de una ejecución material

Result, State, Changes, Files, Verification, Failures, Deviations, Assumptions, Decisions Required y Provenance; indicar no aplica cuando corresponda. No declarar verificaciones no realizadas ni ocultar bloqueos.

Para esta etapa documental basta entregar el archivo, resumir decisiones propuestas y solicitar revisión antes de iniciar planeación.

## 17. Decisiones y siguiente puerta

### Dirección ya aceptada en la conversación

- Skill independiente y complementario a Agent Skills.
- Participación desde especificación y planeación.
- Modos preparación, integración y validación.
- Conversión por capacidad validada y preservación de HITL.
- Integración mediante reglas y artefactos del proyecto, sin editar el plugin.

### Propuestas concretadas aquí, sujetas a revisión de esta especificación

- Política N1/N2/N3 y alcance acotado de N2.
- Sobre JSON único y separación entre resultado y ciclo de vida.
- Campos mínimos de adopción y continuidad.
- Recursos mínimos del futuro paquete y criterios AC-01 a AC-14.

### Decisiones diferidas

- Proyecto piloto y capacidad inicial: se elegirán antes de evaluar integración real.
- Destino de instalación y anfitriones a soportar: se confirmarán antes de instalar.
- Tecnologías, autenticación y proveedor: se resolverán en cada proyecto con evidencia.
- Boilerplate compartido: fuera de esta versión; requiere justificación y aprobación posterior.

No hay una pregunta adicional necesaria para revisar esta especificación. La próxima puerta es su aprobación o solicitud de cambios. Solo después se elaborarán el plan y las tareas de implementación. La creación e instalación del skill requieren autorización del alcance correspondiente.

## 18. Proveniencia y alcance de la verificación

- Instrucciones del usuario y aprobación de la dirección arquitectónica en esta conversación.
- Requerimiento de origen: documento de diseño aportado por el autor, conservado en el expediente privado; no es una dependencia para usar este paquete.
- Agent Skills 0.6.15 instalado: using-agent-skills, spec-driven-development y planning-and-task-breakdown; comandos planning, spec y build; getting-started y manifiesto del plugin.
- Fuente pública del framework consultada durante la evaluación: https://github.com/addyosmani/agent-skills
- Guía de creación de skills disponible en esta sesión: separación de instrucciones, referencias, plantillas y validación futura.

La fuente pública aporta contexto; el análisis de integración se basa en la versión instalada indicada. No se afirma compatibilidad comprobada con versiones posteriores ni con todos los agentes anfitriones.

Verificación de esta entrega: revisión documental de alcance, consistencia y trazabilidad. No se ha creado, instalado, ejecutado ni probado el skill o una aplicación resultante.

