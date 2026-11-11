# Plantilla: sección Automation2App

Usar dentro de la especificación canónica del proyecto, reemplazando campos entre llaves. No copiar instrucciones de plantilla como si fueran decisiones aprobadas. No crear un backlog nuevo.

## Automation2App

- Adopción: {propuesta | aprobada; referencia de aprobación y alcance}.
- Usuario y recorrido: {quién, qué quiere lograr, resultado observable}.
- Entorno previsto: {local, sistema operativo, conectividad y limitaciones}.
- Framework de desarrollo: {Agent Skills instalado, versión comprobada y equivalencias}.
- Fuente canónica: {especificación y sección}.
- Plan y tracker: {rutas o identificadores existentes}.
- Política de autorización: {catálogo, roles, N1/N2/N3 y restricciones adicionales}.
- Proveedor de IA/autenticación: {decisión aprobada con fuentes, o pendiente; no inferir}.
- Evidencia: {ubicación y forma de identificar versión/huellas}.

| Modalidad | Incluida / diferida / excluida | Decisión y condición de inicio |
| --- | --- | --- |
| Interfaz visual | {estado} | {referencia} |
| Conversación de soporte | {estado} | {referencia} |
| Conversación con acciones | {estado} | {referencia} |

| Capacidad ID | Usuario / operación ID | Entradas / salidas | Estado | Evidencia / revisión | Preparación / bloqueos | Tarea |
| --- | --- | --- | --- | --- | --- | --- |
| {ID estable} | {usuario, operación} | {contrato} | {prevista / automatizada-validada / integrada / verificada} | {enlace} | {condiciones pendientes} | {ID del tracker existente} |

El estado no otorga autoridad. Registrar aprobación, bloqueos y permisos aparte. Modalidad y autorización son dimensiones independientes.

### Preparación por capacidad

Registrar evidencia de automatización funcional, entradas/resultados/fallos, contrato estructurado, permisos/precondiciones, dependencias/entorno y aceptación del recorrido. Sin esas condiciones, la integración queda bloqueada.

### Decisiones pendientes

{Decisión, responsable, consecuencia, recomendación y puerta. No convertir esta sección en lista paralela de tareas.}

## Regla breve para el archivo de reglas del proyecto

Añadir solo tras adopción y cambio autorizados. Sustituir la referencia por la ruta o ID real.

> Este proyecto adopta automation2app según {especificación/sección canónica}. Consultar ese skill al especificar o planear capacidades destinadas a usuarios finales y al integrar o validar su interfaz. Durante preparación, documentar la conversión sin implementarla. Conservar las aprobaciones aplicables y retomar estado desde la especificación y el tracker existentes.

El anfitrión determina el archivo de reglas y el mecanismo de invocación; verificarlo antes de escribir. Esta referencia no instala el skill ni cambia permisos.
