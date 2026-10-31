# Despliegue de osTicket con Docker Compose

## ¿Qué es osTicket y para qué sirve?
osTicket es un sistema de gestión de tickets de soporte (Helpdesk) de código abierto. Sirve para centralizar, organizar y enrutar las solicitudes de asistencia técnica que llegan a través de diferentes canales (correo electrónico, formularios web o llamadas telefónicas) hacia una única plataforma web. 

Básicamente, transforma el desorden de los correos electrónicos o mensajes directos en un sistema ordenado de tareas (tickets).

## ¿En qué puede ayudarnos?
Para un equipo enfocado en soporte técnico, gestión de plataformas e instalaciones tecnológicas, osTicket ayuda a:
* **Centralizar incidentes:** Tener un registro único de todos los problemas de hardware, software, redes o VPS reportados.
* **Organizar el trabajo:** Asignar tickets a especialistas específicos y establecer niveles de prioridad.
* **Controlar los tiempos de respuesta (SLA):** Medir cuánto tiempo toma resolver una instalación o atender un reporte de soporte.
* **Crear un historial:** Mantener un registro documentado de las intervenciones previas, soluciones aplicadas y requerimientos de cada área técnica.
* **Evitar la pérdida de tareas:** Al tener un folio para cada solicitud, nada se olvida ni se pierde en bandejas de entrada personales.

## Arquitectura de este proyecto
Este repositorio contiene la configuración para desplegar osTicket en contenedores. El entorno se divide en tres servicios principales[cite: 3]:

1. **db_osticket:** Base de datos MySQL 8.0 encargada de almacenar toda la información del sistema[cite: 3]. Cuenta con configuraciones de seguridad de autenticación nativa y límites de recursos definidos (hasta 0.80 de CPU y 1GB de RAM) para no saturar el servidor[cite: 3].
2. **osticket_web:** La aplicación web (interfaz gráfica) de osTicket expuesta en el puerto 8080[cite: 3].
3. **auto_configurador:** Un servicio auxiliar automatizado que, tras un tiempo de espera de 40 segundos, se conecta a la base de datos para configurar de forma automática el usuario y contraseña del administrador sin requerir intervención manual[cite: 3].

## Cómo levantar el proyecto

1. Clona este repositorio.
2. Crea un archivo llamado `.env` basándote en el archivo de ejemplo (no subas tus contraseñas reales al repositorio público). El archivo `.env` debe contener las siguientes variables[cite: 3]:
   ```env
   MYSQL_ROOT_PASSWORD=tu_password_seguro
   MYSQL_DATABASE=osticket_db
   MYSQL_USER=osticket_user
   MYSQL_PASSWORD=tu_password_db_seguro
   OSTICKET_ADMIN_USER=admin
   OSTICKET_ADMIN_PASSWORD=tu_password_admin_seguro
   OSTICKET_ADMIN_EMAIL=admin@admin.com
3. docker compose up -d #para levanatar los contenedores