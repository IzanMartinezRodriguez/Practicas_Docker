FASE 1: Descarga de la imagen base

Comando: docker pull nginx:alpine

Descripción: Descarga desde el registro oficial de Docker Hub la imagen ligera de Nginx basada en el sistema operativo Alpine Linux. Alpine destaca por su tamaño ultrareducido y su alta seguridad.

FASE 2: Creación del contenedor y prueba inicial

Comandos:
docker create --name alpine-server -it -p 8080:80 nginx:alpine
curl localhost:8080

Descripción:

docker create: Crea el contenedor llamado alpine-server a partir de la imagen descargada sin iniciarlo.

-it: Mantiene una terminal interactiva asignada.

-p 8080:80: Mapea el puerto 8080 del anfitrión al puerto 80 del contenedor.

curl localhost:8080: Prueba el acceso local (falla temporalmente porque el contenedor está detenido).

FASE 3: Arranque del contenedor

Comando: docker start alpine-server

Descripción: Inicia el contenedor alpine-server previamente creado, activando el servicio de Nginx y el mapeo de puertos.

FASE 4: Personalización del servidor web

Comando: docker cp index.html alpine-server:/usr/share/nginx/html

Descripción: Copia el archivo HTML local (index.html) al directorio raíz del servidor web Nginx dentro del contenedor.

FASE 5: Inspección interactiva del contenedor

Comando: docker exec -it alpine-server sh

Descripción: Abre una sesión de intérprete de comandos (sh) interactiva dentro del contenedor en ejecución para verificar los cambios.

FASE 6: Monitoreo de registros (Logs)

Comando: docker logs -f alpine-server

Descripción: Muestra en tiempo real la salida de la consola y los registros de eventos de Nginx. El parámetro -f mantiene el flujo abierto.

FASE 7: Creación de una imagen personalizada (Commit)

Comando: docker commit alpine-server izamarrod/imagen-alpine:a1

Descripción: Congela el estado actual del contenedor y genera una nueva imagen estática local etiquetada como izamarrod/imagen-alpine:a1.

FASE 8: Exportación de la imagen a un archivo físico (Save)

Comando: docker save izamarrod/imagen-alpine:a1 -o imagen-alpine:a1.tar

Descripción: Empaqueta la imagen local en un archivo .tar para respaldarla o transportarla sin necesidad de subirla a Docker Hub.

FASE 9: Limpieza del entorno local

Comandos:
docker rmi izamarrod/imagen-alpine:a1
docker stop alpine-server
docker rm alpine-server

Descripción: Borra la imagen del sistema, detiene el contenedor y elimina definitivamente sus recursos.

FASE 10: Restauración y ejecución final

Comandos:
docker image load -i imagen-alpine:a1.tar
docker run -d -p 8080:80 --name alpine-server izamarrod/imagen-alpine:a1

Descripción: Importa de vuelta la imagen desde el archivo .tar y ejecuta un nuevo contenedor en segundo plano (-d) utilizando la imagen restaurada.
