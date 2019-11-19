FROM ubuntu:18.10
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y
RUN apt-get install -y \
  nano \
  curl \
  wget \
  php-curl \
  php-fpm \
  php-gd \
  php-xsl \
  php-mysqlnd \
  php-cli \
  php-intl \
  php-bz2 \
  php-zip \
  php-mbstring \
  git \
  zip \
  php-apcu \
  php-opcache \
  php-xdebug

RUN wget http://security.ubuntu.com/ubuntu/pool/main/p/php7.2/php7.2-pgsql_7.2.19-0ubuntu0.18.10.1_amd64.deb
RUN wget http://security.ubuntu.com/ubuntu/pool/main/p/php7.2/php7.2-common_7.2.19-0ubuntu0.18.10.1_amd64.deb
RUN apt install ./php7.2-common_7.2.19-0ubuntu0.18.10.1_amd64.deb -y
RUN apt install ./php7.2-pgsql_7.2.19-0ubuntu0.18.10.1_amd64.deb -y
RUN mkdir /run/php
ADD conf/www.conf /etc/php/7.2/fpm/pool.d/www.conf
ADD conf/php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN ln -snf /usr/share/zoneinfo/Europe/Berlin /etc/localtime
RUN echo "xdebug.idekey = PHPSTORM" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.default_enable=1" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_enable=1" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_autostart = 1" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_port = 9001" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_handler = dbgp" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini
RUN echo "xdebug.remote_host = $(getent hosts docker.for.mac.localhost | awk '{ print $1 }')" >> /etc/php/7.2/fpm/conf.d/20-xdebug.ini

WORKDIR /var/www/html/symfony
CMD ["php-fpm7.2"]