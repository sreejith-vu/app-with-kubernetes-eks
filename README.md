# Docker | Image creation | Persistant Volume | Linking Containers | Docker Compose | Creating Network

### Building images and deploying containers.

#### Docker Compose file:
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

#### Creating containers:
```
MacBookPro:docker sreejithvu$ docker-compose up -d
Starting frontend-nginx ... done
Starting backend-app    ... done
```

#### Docker Containers running:
```
MacBookPro:docker sreejithvu$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
090d0c0245df        email-app:aug8      "/bin/sh -c 'python …"   9 minutes ago       Up 9 minutes        5000/tcp             backend-app
46379d8b7abc        nginx:alpine        "nginx -g 'daemon of…"   9 minutes ago       Up 9 minutes        0.0.0.0:80->80/tcp   frontend-nginx
```

#### Application login is working fine, please find logs
#### Container Logs:
```
MacBookPro:docker sreejithvu$ docker logs backend-app
 * Serving Flask app "manage_email_blacklists" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 160-404-759
172.20.0.3 - - [08/Aug/2019 11:38:53] "GET / HTTP/1.0" 401 -
172.20.0.3 - - [08/Aug/2019 11:38:58] "HEAD / HTTP/1.0" 401 -
172.20.0.3 - - [08/Aug/2019 11:39:07] "GET / HTTP/1.0" 401 -
172.20.0.3 - - [08/Aug/2019 11:54:34] "GET / HTTP/1.0" 200 -
172.20.0.3 - - [08/Aug/2019 11:54:34] "GET /static/css/style.css HTTP/1.0" 200 -
172.20.0.3 - - [08/Aug/2019 11:54:39] "POST /search HTTP/1.0" 200 -
172.20.0.3 - - [08/Aug/2019 11:54:39] "GET /static/css/style.css HTTP/1.0" 200 -
```
```
MacBookPro:docker sreejithvu$ docker logs frontend-nginx
172.20.0.1 - - [08/Aug/2019:11:38:53 +0000] "GET / HTTP/1.1" 401 90 "-" "curl/7.54.0" "-"
172.20.0.1 - - [08/Aug/2019:11:38:58 +0000] "HEAD / HTTP/1.1" 401 0 "-" "curl/7.54.0" "-"
172.20.0.1 - - [08/Aug/2019:11:39:07 +0000] "GET / HTTP/1.1" 401 90 "-" "curl/7.54.0" "-"
172.20.0.1 - admin [08/Aug/2019:11:54:34 +0000] "GET / HTTP/1.1" 200 665 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:68.0) Gecko/20100101 Firefox/68.0" "-"
172.20.0.1 - admin [08/Aug/2019:11:54:34 +0000] "GET /static/css/style.css HTTP/1.1" 200 1616 "http://localhost/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:68.0) Gecko/20100101 Firefox/68.0" "-"
172.20.0.1 - admin [08/Aug/2019:11:54:34 +0000] "GET /static/css/favicon.ico HTTP/1.1" 499 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:68.0) Gecko/20100101 Firefox/68.0" "-"
172.20.0.1 - admin [08/Aug/2019:11:54:39 +0000] "POST /search HTTP/1.1" 200 1611 "http://localhost/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:68.0) Gecko/20100101 Firefox/68.0" "-"
172.20.0.1 - admin [08/Aug/2019:11:54:39 +0000] "GET /static/css/style.css HTTP/1.1" 499 0 "http://localhost/search" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:68.0) Gecko/20100101 Firefox/68.0" "-"
```

#### Stopping containers:
```
MacBookPro:docker sreejithvu$ docker-compose down
Stopping frontend-nginx ... done
Stopping backend-app    ... done
Removing frontend-nginx ... done
Removing backend-app    ... done
Removing network docker_default
```

