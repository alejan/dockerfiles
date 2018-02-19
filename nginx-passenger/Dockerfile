FROM ubuntu:16.04
MAINTAINER ServerQuo

RUN apt-get update \
 && apt-get install -y curl unzip 

# JAVA
ARG JAVA_MAJOR_VERSION=8
ARG JAVA_UPDATE_VERSION=131
ARG JAVA_BUILD_NUMBER=11
ENV JAVA_HOME /usr/jdk1.${JAVA_MAJOR_VERSION}.0_${JAVA_UPDATE_VERSION}

ENV PATH $PATH:$JAVA_HOME/bin
RUN curl -sL --retry 3 --insecure \
  --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
  "http://download.oracle.com/otn-pub/java/jdk/${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-b${JAVA_BUILD_NUMBER}/d54c1d3a095b4ff2b6607d096fa80163/server-jre-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz" \
  | gunzip \
  | tar x -C /usr/ \
  && ln -s $JAVA_HOME /usr/java \
  && rm -rf $JAVA_HOME/man

# NGINX 

ENV NGINX_HOME /etc/nginx
ENV NGINX_PACKAGE /usr/sbin
RUN apt-get install -y dirmngr gnupg
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7
RUN apt-get install -y apt-transport-https ca-certificates


RUN echo 'deb https://oss-binaries.phusionpassenger.com/apt/passenger xenial main' > /etc/apt/sources.list.d/passenger.list
RUN apt-get update
RUN apt-get install -y nginx-extras passenger

# PASSENGER

COPY nginx.conf  $NGINX_HOME

CMD $NGINX_PACKAGE/nginx -g "daemon off;"


