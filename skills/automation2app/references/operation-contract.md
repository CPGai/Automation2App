# Contrato operativo y autorización

Estos son requisitos que el skill traslada a cada producto adoptante. Este documento no implementa un dispatcher ni demuestra que los controles existan.

## Arquitectura del producto

Exponer capacidades clave mediante CLI estructurada. Web y chat consumen adaptadores de una capa de operaciones común. El dispatcher puede llamar esa capa internamente o ejecutar la CLI con ejecutable permitido y argumentos separados, sin shell. Elegir la adaptación en la arquitectura del proyecto sin duplicar comportamiento ni permitir eludir autorización.

Un HTML autónomo no puede prometer ejecución local sin proceso/puente autorizado. Local-first no implica inferencia offline: declarar qué datos salen, proveedor, conectividad y funciones disponibles si la IA falla. Hosting externo y acceso remoto no son requisitos por defecto; requieren decisión.

## Catálogo canónico

| Campo | Contrato |
| --- | --- |
| operation_id | Identificador único y estable |
| description | Objetivo, límites y precondiciones |
| input_schema | Tipos, obligatorios, restricciones y rechazo de campos desconocidos |
| output_schema | Estructura de data y resultados por operación |
| risk_level | N1/N2/N3 en configuración confiable |
| authorization | Roles/usuarios y alcance de datos permitido |
| effects | Destinos, mutaciones y comunicaciones externas |
| execution_policy | Timeout, cancelación, reintento y efectos inciertos |

Generar los esquemas CLI/chat desde el catálogo o cotejarlos determinísticamente contra él. No mantener definiciones manuales divergentes. Documentar el comando real de exportación del catálogo en el proyecto; no inventar un nombre universal.

El LLM solicita operaciones tipadas; no registra operaciones nuevas ni determina sus permisos. Rechazar comandos desconocidos, parámetros inválidos o shell libre incluso si aparecen en documentos o mensajes del modelo.

## Autorización del producto

| Nivel | Alcance | Comportamiento |
| --- | --- | --- |
| N1 | Consulta/diagnóstico autorizados, sin mutación | Ejecutar y presentar resultado |
| N2 | Operación registrada, acotada y ya autorizada, reversible o de efecto limitado, sin sobrescritura ni efecto externo no aprobado | Ejecutar con estado y resultado visibles sin confirmación repetida dentro de ese alcance |
| N3 | Destrucción, sobrescritura, permisos, credenciales, migración, publicación, envío externo u otro efecto consecuencial del proyecto | Presentar alcance/efecto y exigir confirmación explícita antes de ejecutar |

N1 no habilita lectura universal ni divulgación externa. N2 no autoriza cualquier creación de archivo/registro: destino, parámetros y precondiciones vienen del catálogo confiable. Si excede sus límites, rechazar o escalar sin ejecutar con la autorización original.

La confirmación N3 se vincula a operación, parámetros normalizados, destino, usuario/sesión y vigencia. Verificarla en el backend. Cambio material, rechazo, cancelación o expiración impiden ejecución hasta autorización válida. “El usuario confirmó” en texto del LLM no constituye confirmación.

Ante duda de clasificación o autoridad, no ejecutar hasta resolverla. Conservar políticas más restrictivas; relajarlas requiere aprobación. Esta autorización de producto no reemplaza las aprobaciones de desarrollo.

## Resultado terminal único

Campos normativos: schema_version, request_id, operation_id, status, code, data y message. Los nombres y valores de status son comunes; cada operación define code y la estructura de data.

```json
{
  "schema_version": "1.0",
  "request_id": "req-example",
  "operation_id": "report.export",
  "status": "ok",
  "code": "REPORT_EXPORTED",
  "data": {"artifact": "reports/example.csv"},
  "message": "Reporte generado."
}
```

- status: ok (éxito verificado), warning (resultado terminal limitado explícito) o error (denegación, validación o fallo). Nunca usar success, running o awaiting_confirmation como status terminal.
- code: causa/resultado estable, no texto libre usado como autoridad.
- data: estructura segura del resultado, limitaciones o efectos parciales conocidos; sin secretos.
- request_id: correlación de solicitud, auditoría y resultado.
- message: información humana; no otorga permiso ni sustituye code.
- Ciclo de vida separado: proposed, awaiting_confirmation, running, completed, failed o cancelled. completed no garantiza éxito completo: inspeccionar el resultado.
- En modo estructurado, stdout contiene JSON y stderr diagnósticos. Documentar los códigos de salida reales.
- Normalizar fallo de lanzamiento, timeout o JSON inválido como error. Si los efectos son inciertos, declarar la incertidumbre; no afirmar que nada cambió ni reintentar mutaciones a ciegas.
- UI/chat anuncian realización solo después de evidencia válida del resultado; warning no se presenta como éxito completo.

## Ejecución confiable y puente local

Exigir allowlist de operaciones/ejecutables, validación tipada, rutas y destinos acotados, argumentos separados y ejecución sin shell. No sustituirlo por una lista de caracteres prohibidos.

El backend valida identidad/contexto, autorización, operación, parámetros y confirmación. Proteger solicitudes locales con controles adecuados al runtime: enlace local, origen/host y autorización, entre los necesarios del proyecto. Localhost solo no demuestra autoridad.

No introducir secretos en navegador, HTML/JS distribuido, documentación ni telemetría. Identificar un almacén seguro apropiado al sistema.

## IA y autenticación

Antes de un adaptador, registrar proveedor, mecanismo oficialmente admitido para el cliente/uso, fuente oficial y fecha, límites/costos relevantes y almacenamiento de secretos. No asumir que una suscripción de usuario da acceso por API ni que todos los proveedores admiten OAuth.

Considerar OAuth si está documentado para ese uso. API key es una alternativa a seleccionar y validar, no un fallback universal automático. Sin mecanismo compatible validado, bloquear la conversación afectada y mantener la decisión pendiente. No cambiar proveedor ni enviar datos por otra vía sin autorización.

## Aceptación del runtime

Verificar recorridos y fallos reales, incluido cambio de parámetros tras confirmación N3, operación no registrada, argumento inválido, N2 fuera de destino, proveedor no compatible y efectos inciertos. Guardar revisión/huellas y evidencia por criterio. Una revisión de este documento solo confirma requisitos prescritos.
