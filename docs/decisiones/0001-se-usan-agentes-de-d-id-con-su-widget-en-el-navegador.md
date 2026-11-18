# 0001. Se usan agentes de D-ID con su widget en el navegador

Estado: aceptado
Fecha: 2026-09-24
Origen: reconstruido desde el historial de git

## Contexto
El proyecto necesita personajes que conversen por voz o texto con avatar de video. Desde el primer commit, cada personaje es un agente de D-ID. Una versión anterior de la página de conversación pedía la configuración de los agentes a un servicio propio (`/api/agents`), que no existe en el sitio estático.

## Decisión
Se usan agentes de D-ID y se cargan con el widget oficial (`agent.d-id.com/v2/index.js`) directamente en el navegador. El ID y la llave de cliente de cada agente se escriben en el objeto `AGENTES` de `agente-embed.html`, sin servicio intermedio. Se conserva el script v2 del widget aunque los agentes usen avatares v4, porque la ruta v4 del script no existe.

## Consecuencias
- El sitio no necesita servidor de aplicación, base de datos ni variables de entorno.
- Las instrucciones, bases de conocimiento, voz y avatar de cada personaje se administran en D-ID Studio, fuera del repositorio.
- La apariencia y los textos del widget dependen de D-ID; la traducción al español se hace con CSS y scripts sobre el widget, y puede romperse cuando D-ID lo actualice.
- Las llaves de cliente quedan visibles en el navegador; su uso se limita con los dominios permitidos de cada agente en D-ID.

## Evidencia
- 66ee1fb Person-AG: login, selector y tres agentes
- 971b97a Restaura agente-embed completo y carga el widget v4 de D-ID (explica que `/api/agents` no existe en el sitio estático)
- c4430fc Regresa el script de D-ID a v2/index.js
- a4253ea Actualiza las 10 llaves de D-ID; incluye marco del nombre y botón
- `agente-embed.html`, objeto `AGENTES`
