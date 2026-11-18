# Operación: Habla con la historia

## Despliegue

1. Integrar los cambios en `main` mediante una solicitud de cambios (pull request, PR) revisada por @ErikV-AG.
2. Railway detecta el push a `main` y despliega el servicio `agentesSEP` en el entorno `production`. Railpack construye el sitio estático y usa el `Caddyfile` del repositorio.
3. Revisar el estado del despliegue en la pestaña Deployments de Railway o en la sección Environments del repositorio en GitHub.
4. Verificar que `https://agentessep-production.up.railway.app/health` responda 200.
5. Abrir un personaje en producción y comprobar que el avatar cargue y responda, tanto desde el selector como con `?modo=saberes`.

No se requieren variables de entorno: Railway asigna `PORT`.

## Reversión

1. En Railway, abrir Deployments del servicio `agentesSEP`, elegir el despliegue anterior que funcionaba y usar Redeploy.
2. Como alternativa, revertir el commit en una rama nueva (`git revert <hash>`), abrir un PR e integrarlo en `main` para que Railway despliegue de nuevo.
3. Verificar con los pasos 4 y 5 de Despliegue.

## Monitoreo

| Señal | Dónde se observa | A quién se avisa |
| --- | --- | --- |
| Despliegue fallido | Railway (Deployments) y GitHub (Environments) | Responsable y supervisión, en `#proj-habla-con-la-historia` |
| `/health` sin respuesta 200 | Navegador o monitor externo. PENDIENTE: ¿hay un monitor configurado? | Responsable |
| Errores del servidor | Registros JSON de Caddy en Railway (Observability) | Responsable |
| Avatar no disponible o sin créditos | Aviso del widget en la página del personaje y panel de D-ID | Responsable y supervisión |

## Tareas periódicas

- Revisar el saldo de créditos de la cuenta de D-ID del proyecto. PENDIENTE: plan, ciclo de facturación y umbral de aviso.
- Revisar el consumo y el pago de Railway. PENDIENTE: plan y titular.
- Revisar los dominios permitidos de cada agente en D-ID cuando cambie la dirección de producción o la de SaberesMX.
- Al cambiar instrucciones o bases de conocimiento en D-ID, actualizar sus fuentes en la carpeta de Drive del proyecto (`03 Fuentes editables`).

## Cambios que requieren consulta

No se modifican sin consultar al responsable y a supervisión:

- El `Caddyfile`.
- El contrato de `?modo=saberes` con SaberesMX.
- Los ID y las llaves de cliente de los agentes en `agente-embed.html`.
- La configuración de los agentes en D-ID.

## Contactos y escalamiento

| Rol | Contacto |
| --- | --- |
| Responsable | @rodrig317-cpu |
| Suplente | PENDIENTE |
| Supervisión y revisión | @ErikV-AG |
| Proveedor de avatares | Soporte de D-ID. PENDIENTE: canal de soporte del plan contratado |
| Hosting | Soporte de Railway |
| Cliente | SEP y UdG. PENDIENTE: contacto del cliente |
| SaberesMX | PENDIENTE: quién mantiene el sitio |
