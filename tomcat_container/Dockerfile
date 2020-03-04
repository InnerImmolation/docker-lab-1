FROM centos:centos7
LABEL maintainer="Dmitry Dubovtsev"

# Install prepare infrastructure
RUN yum -y update && \
 yum -y install wget && \
 yum -y install tar && \
 yum -y install java-1.8.0-openjdk.x86_64

# Prepare environment
ENV JAVA_HOME /
ENV CATALINA_HOME /opt/tomcat
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin:$CATALINA_HOME/scripts

# Install Oracle Java8
RUN yum install java


# Install Tomcat
ENV TOMCAT_MAJOR 8
ENV TOMCAT_VERSION 8.5.50
ENV war_file hello-world.war
ENV user admin
ENV pass admin
ENV server 172.17.0.2
ENV app_name hello-naprimer
RUN wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.50/bin/apache-tomcat-8.5.50.tar.gz && \
 tar -xvf apache-tomcat-8.5.50.tar.gz && \
 rm apache-tomcat*.tar.gz && \
 mv apache-tomcat* ${CATALINA_HOME}

RUN chmod +x ${CATALINA_HOME}/bin/*sh

# Create Tomcat admin user
ADD tomcat-users.xml $CATALINA_HOME/conf/


# Create tomcat user
RUN groupadd -r tomcat && \
 useradd -g tomcat -d ${CATALINA_HOME} -s /sbin/nologin  -c "Tomcat user" tomcat && \
 chown -R tomcat:tomcat ${CATALINA_HOME}

#Deploying test app
RUN rm -rf /opt/tomcat/webapps/ROOT
ADD --chown=tomcat:tomcat ${war_file} ${CATALINA_HOME}/webapps/ROOT.war
#-mount type=bind,source="$(pwd)"/target,target=/app

WORKDIR /opt/tomcat

EXPOSE 8080
EXPOSE 8009

USER tomcat
CMD ["/opt/tomcat/bin/catalina.sh", "run"]
