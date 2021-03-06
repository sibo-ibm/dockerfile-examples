################# Dockerfile for Apache Http Server version 2.4.26 #####################
#
# This Dockerfile builds a basic installation of Apache Http Server.
#
#  The Apache HTTP Server is a powerful and flexible HTTP/1.1 compliant
#  web server.Originally designed as a replacement for the NCSA HTTP
#  Server, it has grown to be the most popular web server on the Internet.
#
# To build this image, from the directory containing this Dockerfile
# (assuming that the file is named Dockerfile):
# docker build -t <image_name> .
#
# To Start ApacheHttpServer use the following command.
# docker run --name <container_name> -p <port_number>:80 -d <image_name>
#
# Test in the browser by using the following url:
# http://<hostname>:<port_number>/
#
########################################################################################

# Base image
FROM s390x/ubuntu:16.04

# The author
MAINTAINER LoZ Open Source Ecosystem (https://www.ibm.com/developerworks/community/groups/community/lozopensource)

ENV SOURCE_DIR=/tmp/source
WORKDIR $SOURCE_DIR

# Install dependencies
RUN apt-get update && apt-get install -y \
	autoconf \
	curl \
	gcc \
	git \
	libexpat1 \
	libexpat1-dev \
	libpcre3-dev \
	libtool-bin \
	libxml2 \
	make \
	openssl \
	python \
	tar \
	wget \

# Clone httpd from git
 && git clone https://github.com/apache/httpd.git && cd httpd && git checkout 2.4.26 \
 
# Download and Install the dependency package apr from source
 && cd $SOURCE_DIR/httpd/srclib && git clone https://github.com/apache/apr.git && cd apr \
 && ./buildconf && ./configure \
 && make && make install \
 
# Build and install httpd
 && cd $SOURCE_DIR/httpd && ./buildconf \
 && ./configure --prefix=/usr/local \
 && make && make install \
 
# Clean up cache , source data and un-used packages
 && apt-get remove -y \
    autoconf \
	curl \
	gcc \
	git \
	libpcre3-dev \
	libtool-bin \
	libxml2 \
	make \
	python \
	wget \
 && apt-get autoremove -y \
 && apt autoremove -y \
 && apt-get clean && rm -rf /var/lib/apt/lists/* $SOURCE_DIR

# Expose port
EXPOSE 80

# Start Apache Http Server
CMD ["apachectl","-D", "FOREGROUND"]

# End of Dockerfile
