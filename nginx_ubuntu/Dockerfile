FROM ubuntu:disco
LABEL maintainer="Dmitry Dubovtsev"
RUN apt-get update && apt-get install nginx-core -y


EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]