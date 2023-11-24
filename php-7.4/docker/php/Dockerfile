FROM php:7.4-fpm-bullseye

COPY ./php.ini /usr/local/etc/php/php.ini

RUN apt-get update \
  && apt-get install -y \
    zip \
    libonig-dev \
    imagemagick \
    libmagickwand-dev \
  && pecl install imagick \
  && docker-php-ext-install \
    mbstring \
    pdo_mysql \
  && docker-php-ext-enable \
    imagick \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && php -r "unlink('composer-setup.php');"

RUN rm -rf /tmp/*
