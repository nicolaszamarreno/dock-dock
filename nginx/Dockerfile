FROM debian:jessie-slim
MAINTAINER Nicolas Zamarreno <zamarreno.nicolas@gmail.com>

RUN apt-get -y update
RUN apt-get install -y wget

RUN echo "deb http://packages.dotdeb.org jessie all" > /etc/apt/sources.list.d/dotdeb.list
RUN wget -O- https://www.dotdeb.org/dotdeb.gpg | apt-key add - apt update
RUN apt-get -y update

RUN apt-get install -y nginx
RUN apt-get install -y php7.0 php7.0-mysql php7.0-curl php7.0-fpm php7.0-json php7.0-intl \
php7.0-sqlite3 php7.0-xml php7.0-zip php7.0-fpm

RUN echo "mysql-server mysql-server/root_password password root" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password root" | debconf-set-selections
RUN apt-get -y install mysql-server

RUN sed -i ";cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.0/cli/php.ini

COPY default /etc/nginx/sites-available/default
COPY xdebug.ini /etc/php/7.0/mods-available/xdebug.ini

EXPOSE 80
EXPOSE 3306

ENTRYPOINT service php7.0-fpm restart && service nginx restart && service mysql restart && /bin/bash