# Dómine

Prototipo de gestión de turnos para clínicas y proyecto personal de Marcos Adrián Acosta Aveiro, estudiante técnico en Informática. Reúne una aplicación web y un trabajo de automatización con n8n, desarrollado con asistencia de herramientas de IA.

## Aplicación web

El archivo `domine-web.zip` contiene el código de la página de reservas, su API en Cloudflare Workers y las migraciones de Cloudflare D1. Permite reservar, consultar, reagendar y cancelar turnos, además de registrar solicitudes de lista de espera. Incluye validación de horarios y controles para evitar reservas superpuestas.

Tecnologías: HTML, CSS, JavaScript, Tailwind CSS, Cloudflare Workers, D1 y Wrangler.

Para ejecutarla, descomprimir domine-web.zip dentro de una carpeta llamada web. Luego, con Node.js 24 instalado:

```sh
cd web
npm ci
npm run db:local
npm run dev
```

Abrir `http://127.0.0.1:8787`. La aplicación necesita su API; abrir solamente el HTML no ejecuta el sistema completo.

```sh
npm test
npm run build
```

El archivo `web/VERIFICACION.md` conserva el alcance y los resultados de verificaciones anteriores, con su fecha. Esas verificaciones no demuestran un despliegue remoto.

## Automatizaciones con n8n

Según el estado informado por el autor, el entorno local usa Docker Desktop, n8n, Evolution API y PostgreSQL. Se crearon dos flujos y se probaron de punta a punta con datos simulados:

- Recordatorio a 24 horas: Schedule Trigger → Google Sheets → Code → HTTP Request → Update row.
- Gestión de respuestas: Webhook → Code → Gemini → Code → Switch. Clasifica confirmación, cancelación o respuesta desconocida; contempla la actualización del turno, la búsqueda de un candidato de lista de espera o una solicitud de aclaración.

Las exportaciones JSON de esos flujos no están incluidas en esta copia: no se localizaron en la carpeta de automatización revisada. Esta descripción documenta el trabajo informado y no sustituye archivos ejecutables.

## Estado y próximos pasos

La web usa D1 y las automatizaciones descritas usan Google Sheets. Son componentes separados: su sincronización no está terminada. La migración de los flujos a la API de la aplicación y D1 está pendiente.

La instancia de Evolution API todavía necesita conectarse con un número de WhatsApp de prueba. El envío real de mensajes no fue verificado. La migración del entorno a un VPS también está pendiente.

Esta copia usa datos demostrativos. Antes de atender pacientes reales se deben completar las integraciones, la configuración de la clínica y las medidas operativas descritas en `web/README.md`.

## Contenido de esta copia

Se incluyen código fuente, configuración de ejemplo, migraciones, pruebas y documentación de la web. Se excluyen dependencias instaladas, bases locales, credenciales, historial Git, archivos de configuración personal del agente y registros de ejecución. No se incluye el `docker-compose.yml` original, que debe revisarse y convertirse en un ejemplo sin credenciales antes de compartirlo.

Todavía no se ha elegido una licencia para el código del proyecto. La visibilidad del repositorio debe decidirse antes de subir esta copia.
