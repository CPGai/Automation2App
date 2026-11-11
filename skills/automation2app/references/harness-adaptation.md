# Adaptar Automation2App a otro anfitrión

## Contenido

- [Objetivo y marco](#objetivo-alcance-y-framework)
- [Estado por destino](#estado-y-límites-de-compatibilidad)
- [Invariantes](#invariantes-portables)
- [Descubrimiento](#descubrimiento-de-adaptación)
- [Adaptación posterior](#adaptación-autorizada-en-fase-posterior)
- [Codex externo](#payload-de-diagnóstico-para-codex-externo)
- [Hermes y Antigravity](#payload-de-diagnóstico-para-hermes-o-antigravity)
- [Continuidad](#entrega-para-una-sesión-futura-de-esta-conversación)

## Objetivo, alcance y framework

Conservar un skill del agente desarrollador que prepara desde especificación/planeación la conversión de automatizaciones en aplicaciones, integra capacidades validadas y verifica recorridos reales. El producto objetivo sigue el patrón CLI estructurada + Web UI local + conversación según alcance aprobado.

Automation2App complementa Agent Skills de Addy Osmani; no lo reemplaza, no se incrusta en un skill genérico de planeación y no dirige un segundo ciclo de desarrollo. El chatbot del producto no es el skill desarrollador. Modalidades de interacción y permisos N1/N2/N3 son independientes.

Esta guía permite evaluar una adaptación sin depender de la conversación de origen. La instalación en cada destino requiere autorización aplicable; el estado y los límites observados se indican a continuación. El contenido portable vive en SKILL.md, las referencias de integración/contrato y la plantilla; agents/openai.yaml es metadato específico de Codex, no un requisito de Hermes o Antigravity.

Base de diseño: SPEC-Automation2App-v0.1.md, aprobada por Carlos el 11 de noviembre de 2026. Fuente pública: https://github.com/CPGai/Automation2App/blob/main/docs/SPEC-Automation2App-v0.1.md
La publicación conserva el diseño aprobado. Codex y Antigravity cuentan con la evidencia limitada descrita en esta matriz; Hermes y otras computadoras requieren validación propia.

## Estado y límites de compatibilidad

| Destino | Información que debe comprobar el agente destino | Estado acreditado por esta entrega |
| --- | --- | --- |
| Codex local examinado | Directorio de usuario y herramientas del anfitrión | Paquete inicializado y validado; copia instalada cotejada; carga por nombre reportada en conversación nativa. Agent Skills 0.6.15 |
| Codex en otra sesión o computadora | Entorno local/Work, checkout y mecanismo de instalación propios; acceso real a Agent Skills | Sin implementar ni verificar |
| Antigravity examinado | Directorio global y capacidades reales del anfitrión | Copia idéntica cotejada; catálogo/carga y compatibilidad documental reportados por AGY con Agent Skills 0.6.13; tres ejercicios del mismo agente. Sin runtime de producto probado |
| Hermes | Catálogo/directorio de skills, invocación, reglas persistentes y herramientas reales | Sin implementar ni verificar |

El usuario indica que otras instancias de Hermes y Antigravity también tienen acceso al plugin Agent Skills. Tratarlo como contexto de intención: comprobar versión, nombres y disponibilidad efectiva antes de depender de ellos. No asumir paridad por compartir nombre de plugin.

Estado observado el 11 de noviembre de 2026; detalles y límites: https://github.com/CPGai/Automation2App/blob/main/docs/VALIDATION.md

Al terminar una adaptación, registrar destino, versión, revisión exacta del contenido, equivalencias y evidencia antes de cambiar esta matriz. No inferir estado a partir de una lista en caché.

## Invariantes portables

- Un skill con preparación, integración y validación; preparación no construye UI.
- Especificación aprobada antes de plan/tareas y plan aprobado antes de implementar, respetando autorización vigente del usuario.
- Integración por capacidad preparada, con evidencia y tarea aprobada.
- Contratos, permisos y comportamiento comunes para CLI, web y chat.
- El modelo del producto propone; el backend valida y autoriza. No terminal general para ese modelo.
- Catálogo canónico y sobre de resultados definido en operation-contract.md.
- Estado desde especificación, plan y tracker existentes; no backlog paralelo.
- No alterar caché/plugin/router global para lograr integración.
- No migrar datos, introducir proveedor/secretos, modificar seguridad o desplegar por el hecho de portar el skill.

Cambiar mecanismos del anfitrión no autoriza cambiar estos invariantes. Una incompatibilidad se documenta y se eleva a decisión, sin fingir compatibilidad.

## Descubrimiento de adaptación

Inspeccionar primero, sin cambios:

1. Identificar anfitrión, versión, sistema operativo y alcance de instalación posible: usuario, proyecto o sesión.
2. Leer sus instrucciones de creación/instalación; resolver rutas reales y comprobar propiedad/escritura. No reutilizar rutas absolutas de otra máquina.
3. Inventariar Agent Skills disponible y mapear las capacidades de agent-skills-integration.md; comprobar cómo leer/invocar un skill sin recursión.
4. Resolver archivo de reglas persistentes, especificación, plan y tracker del proyecto. No crear otro conjunto por diferencias de nombres.
5. Determinar soporte de frontmatter, referencias relativas, metadatos de UI, prompts y política de invocación. Conservar activación útil; no traducir un metadato de Codex como si fuera universal.
6. Identificar herramientas de archivos, CLI y navegador; separar su disponibilidad para el desarrollador de las herramientas del producto.
7. Determinar validadores reales, evaluación aislada y mecanismo de desactivar/revertir solo el paquete nuevo.
8. Presentar matriz observado / supuesto / faltante, cambios mínimos, riesgos y aprobación exacta requerida.

No inventar comandos de instalación, slash commands, opciones de manifiestos ni API de llamadas anidadas. Consultar documentación oficial actual cuando corresponda. Un diagnóstico correcto puede concluir “no soportado todavía”.

## Adaptación autorizada, en fase posterior

Tras aprobación del destino y alcance: preparar una copia identificada del contenido, aplicar solamente adaptaciones de metadatos/rutas/invocación y validar con herramientas reales del anfitrión. Mantener separación entre núcleo portable y adaptador. Registrar cada diferencia y su motivo.

Evaluar al menos: preparación sin construir; plan ajeno preservado; reanudación con cambios detectados; capacidad sin evidencia bloqueada; skill especializado ausente declarado; N3 con parámetros cambiados; shell libre rechazado; fallo/efecto incierto sin éxito inventado. Si solo se evaluaron instrucciones, no afirmar seguridad del runtime.

No instalar ni activar hasta autorización aplicable. Verificar el paquete final y su disponibilidad; conservar mecanismo de desactivación/reversión según el anfitrión, sin eliminar otros skills. No afirmar compatibilidad con una tercera máquina por haber probado una.

## Payload de diagnóstico para Codex externo

Copiar completo al destino; esta guía por sí sola no lo ejecuta.

```text
Intent
Evaluar una adaptación de automation2app a esta instancia de Codex.

Context
Recibir este contenido candidato o el paquete completo: SKILL.md, references/agent-skills-integration.md, references/operation-contract.md, references/harness-adaptation.md, assets/project-adoption.md y agents/openai.yaml. Leer objetivo, alcance e invariantes antes de proponer cambios. La procedencia y estado están en harness-adaptation.md.

Authorized Scope
Solo lectura y propuesta documental. Comprobar instrucciones del anfitrión, destino personal admitido, acceso a Agent Skills y versiones, mecanismos de descubrimiento, reglas persistentes y herramientas/validadores reales. No copiar a un directorio activo ni instalar.

Tasks
Mapear invariantes portables a mecanismos comprobados. Separar núcleo de metadatos propios de Codex. Proponer cambios mínimos, comandos reales, evaluación aislada y reversión. Identificar datos que faltan; no inventarlos.

Acceptance
Diagnóstico autosuficiente para aprobar o rechazar adaptación sin esta conversación. Distinguir observado, supuesto y pendiente. Mantener tres modos, puertas, catálogo/JSON y estado canónico.

Stop Conditions
Cambios de arquitectura, seguridad, alcance, proveedor, gastos, instalación o escritura en proyecto real requieren decisión. No editar plugin/caché ni reproducir credenciales o rutas privadas de otra máquina.

Completion
Result; State; Changes; Files; Verification; Failures; Deviations; Assumptions; Decisions Required; Provenance. Ninguna instalación o compatibilidad se declara comprobada sin evidencia.
```

## Payload de diagnóstico para Hermes o Antigravity

Copiar completo al agente destino. No asumir que un comando de otro anfitrión existe.

```text
Intent
Evaluar automation2app para el anfitrión actual Hermes o Antigravity; identificar cuál y su versión.

Context
Leer el paquete completo o el contenedor documental candidato, especialmente SKILL.md y references/harness-adaptation.md. Objetivo: skill desarrollador complementario a Agent Skills para preparar, integrar por capacidad validada y verificar automatización → aplicación local CLI + Web UI + conversación según alcance.

Authorized Scope
Diagnóstico de solo lectura y propuesta documental; sin instalar, modificar el framework, configurar credenciales o adoptar en proyectos.

Tasks
Comprobar acceso real a Agent Skills, versión/capacidades, directorios/formato/invocación, archivo de reglas, tracker, herramientas y validadores. Mapear el núcleo portable sin duplicar ciclo ni backlog. Identificar metadatos Codex que no aplican. Proponer adaptador mínimo, evaluación aislada, reversión y aprobaciones.

Invariants
Conservar tres modos; preparación sin UI; puertas vigentes; evidencia por capacidad; contratos/autoridad comunes; JSON terminal ok/warning/error; backend autoriza; LLM del producto sin shell libre; no modificar caché/plugin/router global.

Communication
Si caveman está disponible, invocarlo solo como compresión; conservar contratos, negaciones, límites y evidencia completos. Si return-telemetry está disponible, invocarlo para el handoff; de otro modo usar los campos de Completion. No asumir disponibilidad por el nombre del anfitrión.

Acceptance / Stop
Distinguir observado/supuesto/pendiente y compatibilidad propuesta/probada. Parar antes de instalaciones, escrituras reales o cambios de alcance/arquitectura/seguridad. No inventar mecanismos ni garantizar paridad de plugins.

Completion
Result; State; Changes; Files; Verification; Failures; Deviations; Assumptions; Decisions Required; Provenance. Entregar próxima instrucción ejecutable y decisión concreta, sin ejecutar la instalación.
```

## Entrega para una sesión futura de esta conversación

Llevar el paquete/contenedor completo, la especificación aprobada, plan/tracker, hashes y evaluación, bloqueo vigente y autorización del nuevo destino. Reconstituir estado desde esos artefactos. No depender del historial ni de que haya acceso a la misma cuenta o carpeta. Si no se puede transportar el contenido completo, declarar qué falta antes de implementar.
