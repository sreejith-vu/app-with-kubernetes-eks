# Docker | Image creation | Persistant Volume | Linking Containers | Docker Compose | Creating Network

### Step 1. Building images and deploying containers.

Docker Compose file:
```
MacBookPro:docker sreejithvu$ cat docker-compose.yml
version: '3'
services:
  frontend-nginx-srv:
    image: nginx:alpine
    container_name: frontend-nginx
    volumes:
      - ./frontend-nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./frontend-nginx/default.conf:/etc/nginx/conf.d/default.conf
    ports:
      - 80:80

  backend-app-srv:
    build: backend-app/.
    image: email-app:aug8
    container_name: backend-app
    expose:
      - "5000"
```

Creating containers:
```
MacBookPro:docker sreejithvu$ docker-compose up -d
Starting frontend-nginx ... done
Starting backend-app    ... done
```

Docker Containers running:
```
MacBookPro:docker sreejithvu$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
090d0c0245df        email-app:aug8      "/bin/sh -c 'python …"   9 minutes ago       Up 9 minutes        5000/tcp             backend-app
46379d8b7abc        nginx:alpine        "nginx -g 'daemon of…"   9 minutes ago       Up 9 minutes        0.0.0.0:80->80/tcp   frontend-nginx
```

Stopping containers:
```
MacBookPro:docker sreejithvu$ docker-compose down
Stopping frontend-nginx ... done
Stopping backend-app    ... done
Removing frontend-nginx ... done
Removing backend-app    ... done
Removing network docker_default
```

