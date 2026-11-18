# 0003. Se despliega como sitio estático en Railway con un Caddyfile propio

Estado: aceptado
Fecha: 2026-09-24
Origen: reconstruido desde el historial de git

## Contexto
El sitio es un conjunto de páginas HTML sin compilación. Railway lo publica con Railpack, que sirve los sitios estáticos con Caddy. El Caddyfile por defecto de Railpack envía una política de seguridad de contenido (Content-Security-Policy, CSP) que bloquea las direcciones `blob:`, y el widget de D-ID las necesita para el video y el audio del avatar.

## Decisión
Se despliega en Railway con despliegue automático desde `main` y se usa un `Caddyfile` propio en la raíz del repositorio. Ese archivo omite la cabecera CSP a propósito, responde `/health`, oculta archivos de configuración y resuelve rutas sin extensión `.html`.

## Consecuencias
- Cada push a `main` publica el sitio sin pasos manuales.
- El widget de D-ID reproduce video y audio sin bloqueos.
- El sitio no tiene CSP; cualquier cambio al `Caddyfile` se consulta antes con el responsable.
- La dirección de producción depende del nombre del servicio en Railway (`agentessep-production.up.railway.app`).

## Evidencia
- db82dcd Caddyfile propio: permite blob: para el video de D-ID
- `Caddyfile` (comentario de cabecera)
- Despliegues de `railway-app[bot]` en el entorno `agentesSEP / production` registrados en GitHub
