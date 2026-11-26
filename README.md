# Automation2App.V2

**Versión candidata `v2.0.0-rc.1`.** Cuatro skills de agente para convertir una automatización existente en una aplicación local, diseñar su interfaz y verificar las tareas que podrá realizar la persona usuaria. Quien prepara la aplicación elige la skill de entrada según la tarea.

| Quiero… | Empiezo por |
| --- | --- |
| Preparar una conversión, integrar una capacidad aprobada o validar sus operaciones | [Automation2App](skills/automation2app/SKILL.md) |
| Organizar controles, decisiones, estados de error y recuperación | [Progressive WebUI Workflow](skills/progressive-webui-workflow/SKILL.md) |
| Documentar o aplicar la identidad visual aprobada del proyecto | [Design.md](skills/design-md/SKILL.md) |
| Dar dirección visual a una interfaz dentro de esa identidad | [Frontend Design](skills/frontend-design/SKILL.md) |

Por ejemplo, al convertir un generador de reportes en una aplicación, Automation2App identifica el destino del archivo y cuándo pedir confirmación para sobrescribir. Progressive sitúa esa decisión en el recorrido. Design.md aporta las reglas visuales aprobadas y Frontend Design puede aplicarlas al formulario y al resultado. Cada colaboración depende del trabajo pendiente. [Acuerdo entre las cuatro skills](skills/progressive-webui-workflow/references/skill-collaboration.md)

## Probar la candidata

Descarga el código fuente de [la versión candidata](https://github.com/CPGai/Automation2App/releases/tag/v2.0.0-rc.1) y extrae el archivo, o clona la etiqueta en una carpeta nueva:

```shell
git clone --branch v2.0.0-rc.1 --depth 1 https://github.com/CPGai/Automation2App.git Automation2App-rc1
```

1. Para una primera prueba, abre la copia en tu agente y selecciona un `SKILL.md` de la tabla por su ruta. Puedes probarla con la solicitud de abajo.
2. Para instalar el conjunto en un proyecto con Codex, copia las cuatro carpetas completas de `skills/` en `.agents/skills/` del proyecto. Si ya existe una con el mismo nombre, compara las versiones antes de reemplazarla. Abre una sesión nueva y comprueba qué ruta carga el agente al invocar el nombre. Design.md admite invocación explícita mediante `$design-md`.
3. En otro anfitrión, comprueba su mecanismo de carga y la ruta efectiva. El [agente de revisión](agents/frontend-design-agent.md) y la [plantilla de reglas](templates/PROGRESSIVE_UI_RULE_TEMPLATE.md) son recursos opcionales del repositorio.

Solicitud de prueba desde la copia descargada:

```text
Lee skills/automation2app/SKILL.md y usa el modo Preparación. Tengo una CLI local
que genera un reporte con datos ficticios y puede sobrescribir el archivo de
destino. ¿Qué necesita saber la persona antes de confirmar? Documenta el
recorrido y las decisiones pendientes. Detente antes de implementar la interfaz.
```

## Alcance y procedencia

- La [especificación original](docs/SPEC-Automation2App-v0.1.md) y el [contrato operativo](skills/automation2app/references/operation-contract.md) describen los modos de trabajo y la autorización en el backend. El paquete distribuye instrucciones para el agente desarrollador.
- Las pruebas con ejemplos ficticios y sus límites se resumen en [Validación](docs/VALIDATION.md). El [manifiesto](manifest.json) identifica los recursos del paquete por SHA-256.
- Progressive adapta el [framework de CPGai](https://github.com/CPGai/Frontend-Design-Progressive-WebUI-Framework). Design.md es un procedimiento del proyecto que puede trabajar con la [especificación y CLI de Google](https://github.com/google-labs-code/design.md). La CLI es una dependencia opcional para las tareas que la necesiten.
- Frontend Design adapta la [skill de Anthropic](https://github.com/anthropics/skills/tree/main/skills/frontend-design) y conserva su [licencia Apache 2.0](skills/frontend-design/LICENSE.txt). La adaptación documenta la colaboración con las otras skills.
- Automation2App también puede colaborar con [Agent Skills de Addy Osmani](https://github.com/addyosmani/agent-skills). Quien necesite la edición pública anterior de una sola skill puede consultar su [revisión fijada](https://github.com/CPGai/Automation2App/tree/4fd5a5da3fada6a3e876af4b1b786fc5e746b694).
