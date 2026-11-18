# 0002. Se usa una cuenta de D-ID exclusiva para el proyecto

Estado: aceptado
Fecha: 2026-10-06
Origen: informado por el equipo del proyecto durante la incorporación al catálogo

## Contexto
El área tiene otros proyectos que también usan D-ID, como `profesores`. Compartir una sola cuenta haría que el consumo de los personajes de este proyecto agotara los créditos de esos proyectos, y al revés.

## Decisión
Los agentes de Habla con la historia se crean y administran en una cuenta de D-ID separada, dedicada a este proyecto.

## Consecuencias
- El consumo de créditos de este proyecto no afecta a otros proyectos del área.
- Hay una cuenta, un plan y un saldo más que vigilar; sus credenciales se guardan en el gestor de contraseñas del área, grupo habla-con-la-historia.
- Los agentes no pueden moverse a otra cuenta sin recrearlos y cambiar sus ID y llaves en `agente-embed.html`.

## Evidencia
- Información del equipo del proyecto (2026-11-18).
- PENDIENTE: titular y plan de la cuenta.
