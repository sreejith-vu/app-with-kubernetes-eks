FROM nginx:alpine
RUN apk update && apk add vim bash
COPY default.conf /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf
