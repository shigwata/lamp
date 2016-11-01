FROM php:5.6.26-apache
COPY php.ini /usr/local/etc/php/

# jp
RUN sed -i -e "s%http://httpredir.debian.org/debian jessie main%http://ftp.jp.debian.org/debian/ jessie main contrib non-free%g" /etc/apt/sources.list
RUN sed -i -e "s%http://httpredir.debian.org/debian jessie-updates main%http://ftp.jp.debian.org/debian jessie-updates main contrib%g" /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
  git \
  libfreetype6-dev \
  libicu-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng12-dev \
  unzip \
  zip \
  && docker-php-ext-install \
  gd \
  iconv \
  intl \
  mbstring \
  mcrypt \
  pdo_mysql \
  zip \
  && pecl install \
  xdebug \
  && docker-php-ext-enable \
  xdebug

# Install Composer and make it available in the PATH
RUN curl -s https://getcomposer.org/installer | php \
  && mv -v composer.phar /usr/local/bin/composer

RUN composer global require hirak/prestissimo

# apache2
RUN a2enmod rewrite
