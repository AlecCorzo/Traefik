# Traefik

## Actividad: Introducción a Traefik con Docker

### 1. ¿Qué ventaja aporta enrutar por host (dominio) vs por puerto?
El enrutar por el host permite poder acceder a varios servicios usando el mismo puerto y poder diferenciarlos por el dominio o por el subdominio. Esto ayuda a que sea más fácil de manejar y tratar y facilita la escalabilidad
Por otro lado, enrutar por puerto obliga a exponer un puerto diferente por cada servicio, lo cual hace que no escale bien.

### 2. ¿Qué diferencia hay entre labels en los servicios y usar archivos de configuración?
- **Labels en los servicios**: Se definen en el `docker-compose.yml` o en la definición del contenedor. Son dinámicos y permiten que Traefik descubra y configure automáticamente los servicios.
- **Archivos de configuración**: Se guardan en ficheros externos (`traefik.toml`, `traefik.yml`). Son más apropiados para reglas complejas o configuraciones estáticas centralizadas.

### 3. ¿Cómo se entera Traefik de que había servicios nuevos?
Traefik utiliza los **providers** para detectar cambios. Con Docker, se conecta al socket de Docker y escucha los eventos de los de contenedores. De esta manera configura automáticamente los nuevos servicios que tengan labels.

## Evidencias

### Paso 1. Verificar requisitos: Ejecutar en la terminal 'docker --version' y 'docker compose version'. 

![Pantallazo: salida de la terminal con las versiones de Docker y Docker Compose](imagen1.png)

### Paso 2. Levantar Traefik: Crear la configuración mínima y ejecutar 'docker compose up -d' para iniciar Traefik.
![Pantallazo: salida de docker compose ps mostrando que Traefik está corriendo](imagen2.png)

### Paso 3. Acceder al dashboard de Traefik: Abrir en el navegador la URL http://localhost:8080/dashboard/.
![Pantallazo: captura del dashboard de Traefik abierto en el navegador](imagen3.png)

### Paso 4. Desplegar la aplicación de ejemplo: Levantar el servicio de prueba (whoami) para que Traefik lo detecte.
![Pantallazo: terminal mostrando que el servicio de prueba se levantó correctamente](imagen4.png)

### Paso 5. Probar acceso a la aplicación: Acceder en el navegador a http://whoami.localhost o ejecutar curl http://whoami.localhost.
![Pantallazo: evidencia de la respuesta de la aplicación (hostname o IP del contenedor)](imagen4.png)
![Pantallazo: evidencia de la respuesta de la aplicación (hostname o IP del contenedor)](imagen4.png)

### Paso 6. Revisar routers en el dashboard: Ir al dashboard de Traefik a la sección HTTP Routers y confirmar que aparece whoami.localhost
![Pantallazo: captura del dashboard mostrando el router creado para la aplicación](imagen4.png)



