# Habla con la historia (habla-con-la-historia)

Sitio estático en el que estudiantes conversan por voz o texto con personajes históricos de México, agentes con avatar de D-ID, integrados en la sección Habla con la historia de SaberesMX.

## Cómo ejecutar
```bash
git clone git@github.com:Innovacion-AG/habla-con-la-historia.git
cd habla-con-la-historia
python3 -m http.server 8080
# Abrir http://localhost:8080/login.html
# o http://localhost:8080/agente-embed.html?key=leona&modo=saberes
```

## Dónde está todo
- Metadatos del catálogo: catalog-info.yaml
- Arquitectura y dependencias: docs/blueprint.md
- Operación y despliegue: docs/operacion.md
- Decisiones: docs/decisiones/
- Conversación del proyecto: #proj-habla-con-la-historia en Slack

## Reglas para trabajar en este repositorio
- Si un cambio altera la arquitectura, una dependencia externa o un entorno, actualiza docs/blueprint.md en el mismo cambio.
- Si un cambio implica una decisión de proveedor, alcance o enfoque técnico, crea un registro en docs/decisiones/ con estado propuesto.
- Nunca escribas credenciales en el repositorio; registra los nombres de variables en .env.example.
- Al revisar la documentación, actualiza academiaglobal.mx/verificado-el en catalog-info.yaml.
- No modifiques sin consultar al responsable: el Caddyfile, el contrato de `?modo=saberes`, los ID y llaves de los agentes en agente-embed.html ni su configuración en D-ID.
- Cada push a `main` despliega producción en Railway; trabaja en ramas y entrega por solicitud de cambios.
- El repositorio es público: no escribas riesgos, nombres de personas, correos ni datos internos en archivos, mensajes de commit, solicitudes de cambios o incidencias. Los riesgos van al registro RAID de la bitácora ejecutiva.
- Los insumos del cliente y las fuentes editables de los agentes viven en la carpeta de Drive del proyecto, no en el repositorio.
