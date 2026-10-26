# Cambios locales del proxy HCSBA

El 2026-10-26 se versionaron los cambios pendientes del checkout de desarrollo
en `HCSBA-bahmni/bahmni-proxy`, rama `hcsba/development-config`. `upstream`
conserva el repositorio original `Bahmni/bahmni-proxy`.

La rama conserva la base local `0e0aaec`; no incorpora las seis revisiones
posteriores encontradas en `upstream/main` durante esta entrega.

## Contenido preservado

- Configuración local con las dos directivas `upgrade-insecure-requests`
  comentadas y sin redirección automática de HTTP a HTTPS. Esta variante se
  conserva para desarrollo y no implica una configuración para producción.
- Modo `0644` del script de descarga de logging. El Dockerfile lo ejecuta
  explícitamente con `sh`, sin necesitar el bit ejecutable.

## Verificación y publicación

Se comprobó la sintaxis del script con `sh -n` y la configuración con `httpd -t`
en un contenedor temporal de la imagen local `bahmni/proxy:1.1.0`, con los
archivos de esta rama montados como sólo lectura y sin acceso de red.
Resultado: `Syntax OK`; Apache sólo advirtió la ausencia de `ServerName`.

Esta entrega guarda y publica las fuentes; no construye ni despliega una nueva
imagen del proxy. El entorno integrado vigente mantiene su configuración en
`DEV_VERSION/bahmni-docker-HCSBA/bahmni-standard/`, que es distinta de este
archivo de referencia. No se modificaron los servicios en ejecución.
