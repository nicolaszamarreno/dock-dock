FROM debian:jessie-slim
MAINTAINER Nicolas Zamarreno <zamarreno.nicolas@gmail.com>

RUN apt-get update -y

RUN apt-get install -y curl
RUN echo Y | apt-get install -y python-software-properties
RUN curl -sL http://deb.nodesource.com/setup_9.x | bash -
RUN apt-get install nodejs

RUN apt-get install -y nginx
RUN npm install pm2 -g

COPY default /etc/nginx/sites-available/default

EXPOSE 80

ENTRYPOINT service nginx restart && pm2 start /var/www/html/index.js && /bin/bash