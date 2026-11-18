# 0004. Se adopta la interfaz v8 con cuatro grupos de personajes

Estado: aceptado
Fecha: 2026-10-19
Origen: historial de git e información del equipo del proyecto

## Contexto
La interfaz del selector se diseñó fuera de este repositorio, en prototipos publicados en Netlify. Se publicaron, al menos, las versiones v6a, v6b y v8, que se conservan como antecedentes:

- https://agentes-historicos-v6a.netlify.app
- https://agentes-historicos-v6b.netlify.app
- https://agentes-historicos-v8.netlify.app

## Decisión
Se adopta la versión v8 como interfaz del selector (`index.html`). Los personajes se agrupan en cuatro grupos: Política y Estado; Independencia y defensa; Derechos y educación; Letras y pensamiento. El código de los prototipos no se versiona en este repositorio.

## Consecuencias
- `index.html` contiene la v8 completa. Sobre ella se agregaron la verificación de acceso, la activación de los diez personajes, sus GIF de espera con respaldo de iniciales y un ajuste de fechas.
- Los prototipos de Netlify quedan como referencia de diseño; los cambios de interfaz se hacen en este repositorio.
- La v8 y el repositorio hacen referencia a `static/images/LOGO-AG-GRUESO.png`, que no existe en ninguno de los dos; la página lo retira si no carga.

## Evidencia
- 38423a3 Nueva interfaz (2026-10-19)
- 4af9856 Activa tarjetas de Tlacaelel, Matilde y Rulfo
- Comparación del 2026-11-18 entre https://agentes-historicos-v8.netlify.app e `index.html`: mismos cuatro grupos y mismos diez personajes.
