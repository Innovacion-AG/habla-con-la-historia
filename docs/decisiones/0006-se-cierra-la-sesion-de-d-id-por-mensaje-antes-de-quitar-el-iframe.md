# 0006. Se cierra la sesión de D-ID por mensaje antes de quitar el iframe

Estado: propuesto
Fecha: 2026-11-19
Origen: propuesta del equipo del proyecto

## Contexto
SaberesMX monta `agente-embed.html?key=<personaje>&modo=saberes` en un iframe solo mientras la videollamada está abierta. Al cerrarla, quita el iframe sin aviso. La sesión de D-ID puede quedar abierta y ocupar un lugar del plan hasta que D-ID la expire.

Los agentes son V4: se conectan por LiveKit y no envían `DELETE /streams` al salir. La API del widget no tiene una función para colgar, y `cerrarSesion()` solo apaga las pistas de audio y video. La salida limpia es el botón «Terminar conversación» del widget (aria-label original «End call»), y su cierre es asíncrono: necesita unos instantes antes de quitar el iframe.

## Decisión
El contrato de `?modo=saberes` incorpora un protocolo de cierre por `postMessage`:

1. El sitio padre oculta el iframe y le envía `{tipo: 'cerrar-sesion'}`.
2. `agente-embed.html` pulsa «Terminar conversación», espera el evento `connection` en `'disconnected'` con un tope de 2.5 s, llama a `cerrarSesion()` y responde `{tipo: 'sesion-cerrada'}`. Si la conexión está en `'connecting'`, espera a `'connected'` dentro del mismo tope y entonces pulsa el botón. Sin conversación activa, responde de inmediato.
3. El sitio padre quita el iframe al recibir la respuesta o a los 3 s, lo que ocurra primero.

El embed solo atiende el mensaje con `?modo=saberes`, dentro de un iframe y si viene de `window.parent`. Responde al origen del mensaje, nunca a `'*'`. Si llegan varios pedidos, pulsa el botón y responde una sola vez. Sin el mensaje, la página funciona como antes.

## Consecuencias
- Requiere que SaberesMX adopte el cambio en su página. Mientras no lo haga, el comportamiento es el actual.
- Quitar el iframe puede tardar hasta 3 s después de cerrar la videollamada. El iframe se oculta desde el primer momento, así que la espera no se ve.
- Depende del botón del widget. Si D-ID cambia su aria-label o su comportamiento, el embed no lo encuentra o no recibe la desconexión, espera el tope y la sesión puede quedar abierta como hoy.
- El embed escucha el evento `connection` de la API del widget por su cuenta, aparte del micrófono manual.

## Evidencia
- Pruebas del 2026-11-19 con un widget simulado y una página padre en otro origen, fuera del repositorio:
  - con conversación activa, el padre recibe la respuesta y quita el iframe en unos 0.6 s;
  - sin conversación activa, la respuesta es inmediata;
  - con la conexión en curso, el embed espera a que conecte, pulsa el botón y responde; si no llega a conectarse, responde al vencer el tope;
  - si D-ID no confirma la desconexión, el embed responde al vencer su tope de 2.5 s;
  - si el embed no responde, el padre quita el iframe a los 3 s;
  - con varios pedidos, el botón se pulsa una sola vez y hay una sola respuesta;
  - se ignoran los pedidos de otro iframe, los mensajes de otro tipo y la página abierta fuera de un iframe.
- PENDIENTE: prueba con D-ID real.
