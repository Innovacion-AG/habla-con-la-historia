# 0005. Se mantiene el control de acceso por código en el navegador

Estado: aceptado
Fecha: 2026-11-18
Origen: historial de git y confirmación del equipo del proyecto durante la incorporación al catálogo

## Contexto
El selector propio se protege con un código de cuatro dígitos. La validación ocurre en el navegador (`login.html`) y la sesión se marca en `sessionStorage`. La integración en SaberesMX carga cada personaje con `?modo=saberes`, que no pide código porque el acceso lo controla el sitio de SaberesMX.

## Decisión
Se mantiene el control de acceso tal como funciona hoy: código en `login.html`, marca de sesión en el navegador y modo SaberesMX sin código.

## Consecuencias
- El sitio sigue siendo estático, sin servidor de aplicación ni cuentas de usuario.
- La integración con SaberesMX no requiere que las personas usuarias escriban un código.
- El código es compartido: no identifica a cada persona ni permite revocar accesos de forma individual.
- Los riesgos asociados se registran en el registro RAID de la bitácora ejecutiva (acceso interno).

## Evidencia
- 66ee1fb Person-AG: login, selector y tres agentes
- 4aefef1 GIF en reposo de Leona en su marco (introduce `?modo=saberes`)
- `login.html`, `index.html` y `agente-embed.html` (verificación de `ag_auth`)
