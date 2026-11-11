# Automation2App

Skill para preparar, integrar y validar la conversión de automatizaciones o CLI
en aplicaciones operables mediante Web UI local y, cuando se apruebe,
asistencia conversacional.

Complementa [Agent Skills de Addy Osmani](https://github.com/addyosmani/agent-skills).
El framework se instala y comprueba por separado; este repositorio distribuye
Automation2App y su documentación.

## Modos

| Modo | Resultado |
| --- | --- |
| Preparación | Incorporar requisitos desde especificación y planeación, sin construir la UI |
| Integración | Conectar una capacidad cuya automatización y tarea estén validadas/aprobadas |
| Validación | Comprobar recorridos, contratos, permisos y fallos con evidencia |

CLI, web y chat comparten operaciones y autorización. El modelo del producto
propone llamadas tipadas; el backend confiable valida y autoriza. Se conserva
HITL para acciones consecuenciales. No se incluye servidor, chatbot, CLI de
producto ni selección predeterminada de proveedor o framework web.

## Contenido

- [Skill y selección de modo](skills/automation2app/SKILL.md).
- [Integración con Agent Skills](skills/automation2app/references/agent-skills-integration.md).
- [Contrato operativo y N1/N2/N3](skills/automation2app/references/operation-contract.md).
- [Guía de adaptación](skills/automation2app/references/harness-adaptation.md).
- [Plantilla de adopción](skills/automation2app/assets/project-adoption.md).
- [Especificación](docs/SPEC-Automation2App-v0.1.md).
- [Validación, procedencia y límites](docs/VALIDATION.md).
- [Huellas del paquete](manifest.json).

## Instalación local

Revisar primero las instrucciones y ubicaciones admitidas por la versión del
anfitrión. Instalar este skill es una decisión separada de adoptarlo en un
proyecto o autorizar operaciones de una aplicación.

Clonar el repositorio o descargar sus archivos. Copiar la carpeta completa
`skills/automation2app`, conservando sus seis recursos, en el directorio de
skills elegido. No copiar el repositorio completo dentro de la carpeta del skill.

| Anfitrión examinado | Destino de usuario | Invocación que debe comprobarse |
| --- | --- | --- |
| Codex local | `~/.codex/skills/automation2app/` | `$automation2app` |
| Antigravity | `~/.gemini/config/skills/automation2app/` | Invocación por nombre o `/automation2app`, según superficie/version |
| Otro anfitrión o computadora | Descubrir destino y mecanismo reales | Validar con la guía de adaptación |

Ejemplo PowerShell para Codex, ejecutado desde la raíz de esta copia:

```powershell
$skillDestination = Join-Path $env:USERPROFILE '.codex\skills\automation2app'
if (Test-Path -LiteralPath $skillDestination) { throw 'El destino ya existe; comparar antes de reemplazar.' }
New-Item -ItemType Directory -Path (Split-Path -Parent $skillDestination) -Force | Out-Null
Copy-Item -LiteralPath '.\skills\automation2app' -Destination $skillDestination -Recurse
```

Para Antigravity, usar como destino `.gemini\config\skills\automation2app`
bajo el perfil de usuario. `agents/openai.yaml` es metadato de Codex, conservado
en el paquete; no le otorga autoridad sobre otros anfitriones.

Después comprobar por separado: hashes/estructura, presencia en catálogo,
carga por nombre y comportamiento documental. Una carpeta presente no acredita
descubrimiento. El agente debe declarar capacidades o procesos ausentes.

## Uso y adopción

Indicar la intención y la fase del proyecto al invocar Automation2App. Leer el
estado desde la especificación, plan y tracker existentes. La plantilla de
adopción se incorpora a la especificación canónica tras aprobación; no crea
un segundo backlog ni modifica Agent Skills o reglas globales automáticamente.

Para comprobar solo disponibilidad:

```text
Usa automation2app solo para comprobar que puedes resolverlo por nombre.
Indica su ruta de carga, sus tres modos y recursos. No modifiques archivos,
no adoptes el patrón y no inicies una aplicación ni un piloto.
```

La validación del skill documental no prueba la seguridad o funcionalidad de
un backend real. El proyecto adoptante debe ejecutar sus propios recorridos y
pruebas de autorización. Ver el alcance exacto en [VALIDATION.md](docs/VALIDATION.md).
