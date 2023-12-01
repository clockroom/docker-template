FROM php:8.1-fpm-bullseye

RUN apt-get update

RUN apt-get install -y \
    libmagickwand-dev \
    libonig-dev \
  && pecl install imagick \
  && docker-php-ext-install \
    mbstring \
    pdo_mysql \
  && docker-php-ext-enable \
    imagick

RUN apt-get install -y \
    imagemagick \
    zip \
  && curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin \
    --filename=composer

RUN apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/*

COPY ./php.ini /usr/local/etc/php/php.ini
