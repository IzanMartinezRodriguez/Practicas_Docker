FASE 1
  $docker pull nginx:alpine
FASE 2
    docker create --name alpine-server -it -p 8080:80 nginx:alpine

    curl localhost:8080
    
FASE 3
    docker start alpine-server 
FASE 4
    docker cp index.html alpine-server:/usr/share/nginx/html
FASE 5
    docker exec -it web-server sh
FASE 6
    docker logs -f alpine-server
FASE 7
    docker commit alpine-server izamarrod/imagen-alpine:a1
FASE 8
    docker save izamarrod/imagen-alpine:a1 > imagen-alpine:a1
FASE 9
    docker rmi izamarrod/imagen-alpine:a1
    docker stop alpine-server
    docker rm alpine-server
FASE 10
    docker image load -i imagen-alpine:a1
    docker run -d -p 8080:80 --name alpine-server izamarrod/imagen-alpine:a1







