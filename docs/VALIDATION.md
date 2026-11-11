# Validación y límites

Fecha de observación: 11 de noviembre de 2026.

## Qué distribuye este repositorio

Un skill documental con seis recursos, más documentación de uso y diseño. No
contiene un runtime de producto ni los registros personales del entorno donde
se desarrolló. Los metadatos y rutas de instalación pertenecen a cada anfitrión.

## Evidencia disponible

| Superficie | Evidencia | Límite |
| --- | --- | --- |
| Estructura del candidato original | Inicializador y generador de metadatos locales; validador oficial Codex exit 0; PyYAML 6.0.3; enlaces y JSON válidos | No prueba decisiones correctas ni ejecución de una aplicación |
| Comportamiento documental Codex | Seis evaluaciones con contextos independientes, 14 criterios AC-01–AC-14 satisfechos según sus registros | Escenarios sintéticos, sin runtime de producto |
| Instalación Codex | Seis recursos cotejados con fuente y commit; validador sobre copia final exit 0 | Alcance del equipo observado |
| Descubrimiento Codex | Respuesta nativa aportada por el usuario: resolución por nombre, ruta, modos y recursos | Evidencia aportada; no se conserva aquí un trace/ID de la conversación; selección automática no probada por separado |
| Integridad Antigravity | Copia de seis recursos con hashes iguales; cotejo posterior de esta publicación | No equivale a pruebas del backend |
| Descubrimiento/colaboración AGY | Reporte del agente AGY: catálogo cargado, Antigravity CLI 1.5.0 y Agent Skills 0.6.13 con procesos pertinentes disponibles | Declaración del agente en su expediente; no auditoría independiente del anfitrión |
| Comportamiento AGY | Tres ejercicios simulados del mismo agente: falta de especificación, falta de evidencia e invalidación N3 | No evaluación independiente; los resultados JSON/acciones son ilustrativos, no ejecuciones reales |

La base de integración examinada en Codex fue Agent Skills 0.6.15. AGY reportó
compatibilidad documental con 0.6.13. No se afirma paridad universal entre
versiones. Hermes y otras computadoras siguen sin implementación verificada.

AGY no tenía PyYAML en su Python estándar: realizó comprobaciones de hashes,
enlaces y JSON. Eso no se presenta como parseo YAML completo independiente.
La identidad de bytes vincula esa copia al candidato que sí pasó el parser y
el validador oficiales en Codex.

## Procedencia de esta edición pública

La huella agregada del paquete original instalado es:
`5eba5aca5c4d2d2b69eb7d934b1c43af16f4967b9be55bb5fb14645f8110d63c`.

Cinco recursos se publican sin cambios. La guía `references/harness-adaptation.md`
solo actualiza el estado de los anfitriones y sustituye una referencia privada
por la especificación pública. No cambia modos, contratos, autorización ni
procedimientos. Las instalaciones existentes se conservan intactas.

La especificación se publica como edición documental, retirando una referencia
privada y señalando su aprobación y el estado posterior. No cambia el diseño.
Las huellas finales de los seis recursos están en [manifest.json](../manifest.json).
La validación estructural de la carpeta pública y sus referencias se ejecutó
antes de publicarla; los comandos/resultados precisos se conservaron en el
expediente local de publicación.

## Qué sigue sin probarse

- Aplicaciones, backend, bridge local, navegador o proveedores de IA reales.
- Seguridad implementada de N1/N2/N3: el skill prescribe controles, no los ejecuta.
- Selección automática sin invocación explícita en todos los anfitriones.
- Compatibilidad universal, otras máquinas o futuros cambios del framework.
- Instalación en Hermes o un piloto real G3.

## Fuentes del framework y anfitrión

- https://github.com/addyosmani/agent-skills
- https://github.com/addyosmani/agent-skills/blob/main/docs/antigravity-setup.md
- https://antigravity.google/docs/skills
- https://antigravity.google/docs/customization-discovery
