# Habla con la historia

Sitio web en el que estudiantes conversan, por voz o por texto, con diez personajes históricos de México. Cada personaje es un agente conversacional con avatar de D-ID. El sitio se integra en la sección «Habla con la historia» de SaberesMX y también tiene un selector propio con código de acceso.

## Estado y responsables

| Dato | Valor |
| --- | --- |
| Estado | Piloto (solo pruebas, sin usuarios reales) |
| Criticidad | Alta |
| Cliente y patrocinio | SEP y Universidad de Guadalajara (UdG) |
| Responsable | @rodrig317-cpu |
| Suplente | @CoriaAlx |
| Supervisión y revisión | @ErikV-AG |
| Producción | https://agentessep-production.up.railway.app |
| Credenciales | Gestor de contraseñas del área, grupo habla-con-la-historia |

## Arranque

El sitio es HTML, CSS y JavaScript sin compilación ni dependencias que instalar.

1. Clonar el repositorio:
   ```bash
   git clone git@github.com:Innovacion-AG/habla-con-la-historia.git
   cd habla-con-la-historia
   ```
2. Servir la carpeta con cualquier servidor estático. Con Python 3:
   ```bash
   python3 -m http.server 8080
   ```
   Para reproducir producción con exactitud, usar Caddy con el `Caddyfile` del repositorio:
   ```bash
   PORT=8080 caddy run --config Caddyfile --adapter caddyfile
   ```
3. Abrir `http://localhost:8080/login.html` y escribir un código de acceso. El código se solicita en `#proj-habla-con-la-historia`.
4. Elegir un personaje en el selector. Para probar el modo integrado de SaberesMX, que no pide código, abrir `http://localhost:8080/agente-embed.html?key=leona&modo=saberes`.
5. Verificar que el avatar cargue y responda. Requisito: el dominio desde el que se sirve debe estar permitido en la configuración de cada agente en D-ID. PENDIENTE: ¿`localhost` está entre los dominios permitidos?

## Estructura del repositorio

| Ruta | Contenido |
| --- | --- |
| `index.html` | Selector de personajes en cuatro grupos (interfaz v8) |
| `login.html` | Pantalla de código de acceso |
| `agente-embed.html` | Conversación con un personaje: carga el widget de D-ID según `?key=<personaje>` y admite `?modo=saberes` |
| `saberes.html` | Reproducción de la página «Retratos Urbanos» del sitio de pruebas de SaberesMX, para probar la integración |
| `static/images/` | GIF de espera de cada personaje |
| `Caddyfile` | Configuración del servidor Caddy en Railway |

Las instrucciones y bases de conocimiento de los agentes se editan en D-ID Studio. Sus fuentes editables están en la carpeta de Drive del proyecto, en `03 Fuentes editables`; la versión vigente es `v2`.

## Documentación

- [Blueprint: arquitectura, dependencias y entornos](docs/blueprint.md)
- [Operación: despliegue, reversión y monitoreo](docs/operacion.md)
- [Registros de decisiones](docs/decisiones/)
- [Ficha del catálogo](catalog-info.yaml)

## Dónde pedir ayuda

Canal de Slack `#proj-habla-con-la-historia`.
