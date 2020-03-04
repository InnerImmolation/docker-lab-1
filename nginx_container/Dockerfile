FROM centos:centos7
LABEL maintainer="Dmitry Dubovtsev"
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-12.noarch.rpm
RUN yum -y install nginx \
yum clean all

COPY templates/nginx.conf /etc/nginx/
COPY templates/tomcat.conf /etc/nginx/conf.d/
RUN ln -s /dev/stdout /var/log/nginx/access.log && \
    ln -s /dev/stderr /var/log/nginx/error.log
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]
