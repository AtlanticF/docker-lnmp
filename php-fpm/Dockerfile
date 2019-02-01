FROM php:5.6-fpm

WORKDIR "/app"

COPY ./sources.list /etc/apt/sources.list

# 安装 php 扩展
RUN apt-get update && apt-get install -y --no-install-recommends --assume-yes \
         apt-utils \
         zip unzip vim wget curl \
         libfreetype6-dev \
         libmcrypt-dev \
         libjpeg62-turbo-dev \
         libpng-dev \
         libevent-dev \
         libmemcached-dev \
         zlib1g-dev \
         libmagickwand-dev \
         imagemagick libmagick++-dev \
    && mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd sockets zip \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install sysvsem \
    && docker-php-ext-install sysvshm \
    && docker-php-ext-install sysvmsg \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install mysql \
    && docker-php-ext-install mcrypt \
    && pecl install memcache && docker-php-ext-enable memcache \
    && pecl install redis && docker-php-ext-enable redis \
    && pecl install imagick && docker-php-ext-enable imagick

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*