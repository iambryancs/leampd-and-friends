#
#+++++++++++++++++++++++++++++++++++++++++++++++
# Image setup
#+++++++++++++++++++++++++++++++++++++++++++++++
#

FROM php:7.2-fpm

LABEL maintainer="Bryan CS <yanser25@gmail.com>"

#
#+++++++++++++++++++++++++++++++++++++++++++++++
# Software setup
#+++++++++++++++++++++++++++++++++++++++++++++++
#
RUN apt-get update \
  && apt-get install -y git zip unzip --no-install-recommends \
    curl \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
  && rm -rf /var/lib/apt/lists/*

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql \
# Install the PHP zip extension
    && docker-php-ext-install zip \
# Install the PHP gd library
    && docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-jpeg-dir=/usr/lib \
        --with-freetype-dir=/usr/include/freetype2 && \
        docker-php-ext-install gd

# Install redis php extension
RUN printf "\n" | pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"