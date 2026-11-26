---
name: design-md
description: "Captura la identidad de una marca y crea, valida o aplica el DESIGN.md de un proyecto mediante la CLI de Google. Uso bajo demanda."
---

# DESIGN.md por proyecto

Invocación: `$design-md` seguida del proyecto y la tarea: capturar, definir, validar, aplicar o comparar. Ejecuta solamente las etapas solicitadas; si el proyecto no está identificado, pregunta por su carpeta o URL antes de escribir resultados.

La skill es global; los datos, decisiones y diseños pertenecen a cada proyecto. No guardes marcas en esta carpeta ni cambies instrucciones globales. Este procedimiento combina captura propia inspirada en Pomelli con el formato y la CLI de Google; no es un workflow oficial de Google.

## Capturar y definir

Lee [capture-brand.md](references/capture-brand.md) cuando sea necesario identificar o actualizar la marca. Reutiliza primero el DESIGN.md y las fuentes existentes. Conserva la identidad actual salvo que se solicite rediseño.

Guarda las fuentes, observaciones, inferencias, propuestas y decisiones en `docs/brand/brand-profile.md` del proyecto. Crea el borrador en `docs/brand/DESIGN.draft.md` si falta aprobación de la identidad; conserva cualquier DESIGN.md aprobado. Presenta el perfil y una muestra visual pequeña antes de adoptar por primera vez el diseño o cambiar su identidad. La confirmación se refiere a esa propuesta concreta; no se repite para aplicar un diseño ya aprobado dentro de la tarea autorizada.

Tras esa revisión, guarda `DESIGN.md` en la raíz del proyecto. Incluye valores exactos y criterios de aplicación; el perfil conserva la evidencia y las dudas. No copies información desconocida como si estuviera confirmada.

## CLI de Google

Versión base comprobada en Windows: `@google/design.md@0.4.0` (Node >=18). Comprueba `node --version`. Si el proyecto ya registra otra versión, respétala y verifica su compatibilidad. Registra la versión utilizada en el perfil y reutilízala en sesiones posteriores. No actualices silenciosamente; al solicitar una actualización, consulta `npm view "@google/design.md" version engines --json` y prueba la nueva versión antes de adoptarla.

En PowerShell usa el alias sin punto `designmd`. Ajusta las rutas al proyecto:

```powershell
npx --yes --package="@google/design.md@0.4.0" designmd spec
npx --yes --package="@google/design.md@0.4.0" designmd lint .\DESIGN.md
npx --yes --package="@google/design.md@0.4.0" designmd diff .\DESIGN-before.md .\DESIGN.md
npx --yes --package="@google/design.md@0.4.0" designmd export --format css-tailwind .\DESIGN.md
```

Consulta `spec` al crear o actualizar el formato; consulta `--help` si la versión seleccionada tiene opciones diferentes. Google mantiene la especificación en https://github.com/google-labs-code/design.md y https://github.com/google-labs-code/design.md/blob/main/docs/spec.md.

Ejecuta lint antes de exportar. Corrige errores y evalúa advertencias: una salida exitosa no implica ausencia de advertencias ni aprobación visual. Si la CLI falla por red o instalación, informa el bloqueo y conserva el borrador; no declares validación exitosa. No elimines cachés ni cambies el registro npm para sortear el fallo.

## Aplicar y comparar

Lee el DESIGN.md aprobado y el stack del proyecto. Exporta solo el formato pertinente: `json-tailwind` para Tailwind v3, `css-tailwind` para v4, o `dtcg` para intercambio. En otros stacks, traduce los valores al sistema de estilos existente.

Antes de cambiar un archivo aprobado, conserva una copia en la carpeta de trabajo del proyecto y compara con `diff`. El resultado de diff refleja hallazgos técnicos, no toda diferencia visual o semántica; revisa también los cambios reales. Escribe exportaciones primero a un archivo nuevo, comprueba su contenido y luego intégralo sin reemplazar estilos ajenos a la tarea.

Aplica el diseño solo a las pantallas o componentes solicitados. Verifica en el navegador la muestra o pantalla modificada, incluyendo tamaño móvil cuando corresponda, y reporta qué se comprobó. Lint no sustituye las comprobaciones visuales, de interacción y de accesibilidad.

Si el trabajo requiere reorganizar la interacción, usar `progressive-webui-workflow` para revisar jerarquía, controles y recorridos; si requiere dirección artística, usar `frontend-design` dentro de la identidad aprobada. Resolverlos por nombre y capacidad disponible. Entregarles las reglas vigentes, alcance de pantallas y decisiones visuales abiertas; registrar sus propuestas nuevas en borrador/perfil, las reglas aprobadas en DESIGN.md y las brechas de interacción en la tarea del proyecto. No crear una segunda fuente de tokens ni adoptar cambios de identidad sin la revisión concreta ya definida. Si falta un colaborador, declarar la limitación y usar un proceso equivalente dentro del alcance, sin fingir invocación ni instalarlo por este enlace.

Devolver reglas, propuestas y evidencia al responsable de la tarea sin reiniciar el workflow, reinvocar al colaborador en bucle ni repetir aprobaciones ya cubiertas. No adoptar `automation2app` por una tarea visual; cuando ya esté adoptado, respetar sus operaciones, efectos y autorizaciones y devolverle las brechas del contrato operativo. Leer una identidad aprobada no obliga a recapturar marca ni ejecutar CLI fuera de la tarea solicitada. Estos enlaces no amplían el alcance de pantallas ni habilitan una implementación completa por haber pedido una muestra.

Entrega rutas del perfil y diseño, estado borrador/aprobado, versión de CLI, resultado de validación, cambios realizados y pendientes concretos. No declares instalado, probado o aprobado lo que no hayas verificado.
