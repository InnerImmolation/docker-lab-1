FROM alpine:latest
LABEL maintainer="Dmitry Dubovtsev"
RUN apk update && apk add nginx
RUN mkdir -p /run/nginx

EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]