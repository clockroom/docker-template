FROM php:8.3-fpm-bullseye

RUN apt-get update && apt-get install -y \
    libmagickwand-dev \
    libonig-dev \
    libzip-dev \
  && pecl install \
    imagick \
  && docker-php-ext-install \
    gd \
    mbstring \
    pdo_mysql \
    zip \
  && docker-php-ext-enable \
    imagick \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN apt-get update && apt-get install -y \
    imagemagick \
    zip \
  && curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin \
    --filename=composer \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./php.ini /usr/local/etc/php/php.ini
