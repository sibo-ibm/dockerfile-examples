################################# Dockerfile for NGINX 1.12.0 #####################################################
#
# This Dockerfile builds a basic installation of NGINX.
# NGINX is a free, open-source, high-performance HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server.
#
# To build this image, from the directory containing this Dockerfile
# (assuming that the file is named Dockerfile):
# docker build -t <image_name> .

# To create container of NGINX image run the below command
# docker run --name <container name> -d <nginximage>
#
# To create container of NGINX image run the below command
# docker run --name <container name> -p <port_number>:80 -d <nginximage>
# To view the default nginx website open the link http://<hostname>:<port_number>                                                   
###############################################################################################################
# Base image
FROM s390x/ubuntu:16.04

# The author
MAINTAINER LoZ Open Source Ecosystem (https://www.ibm.com/developerworks/community/groups/community/lozopensource)

WORKDIR "/root"

# Installing dependencies and NGINIX
RUN apt-get update && apt-get install -y \
	gcc \
	libpcre3-dev \
	libssl-dev \
	make \
	openssl \
	tar \
	wget \	
 && wget http://nginx.org/download/nginx-1.12.0.tar.gz \
 && tar xvf nginx-1.12.0.tar.gz \
 && cd nginx-1.12.0 \
 && ./configure \
 && make  \
 && make install  \
 
# Clean up Cache data , unused packages and source files 
 && apt-get remove -y \
	make \
	wget \
 && apt-get autoremove -y && apt-get clean \
 && rm -rf /root/nginx-1.12.0.tar.gz  /root/nginx-1.12.0 \
 && rm -rf /var/lib/apt/lists/*

# Add VOLUMEs to allow backup error logs, configuration and server directory content
VOLUME  ["/var/log/nginx/","/etc/nginx","/var/www/html"]

# For standard non-secured "http" is port 80, Netscape chose 443 to be the default port used by secure http.
EXPOSE 80 443 8080

# Start NGINX Server
CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]

# End of Dockerfile
