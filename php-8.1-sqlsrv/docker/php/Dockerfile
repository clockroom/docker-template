FROM php:8.1-fpm-bullseye

RUN apt-get update && apt-get install -y \
    libmagickwand-dev \
    libonig-dev \
  && pecl install imagick \
  && docker-php-ext-install \
    mbstring \
    pdo_mysql \
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

RUN curl -sS https://packages.microsoft.com/keys/microsoft.asc | tee /etc/apt/trusted.gpg.d/microsoft.asc \
  && curl -sS https://packages.microsoft.com/config/debian/11/prod.list | tee /etc/apt/sources.list.d/mssql-release.list \
  && apt-get update && ACCEPT_EULA=Y apt-get install -y \
    msodbcsql18 \
    unixodbc-dev \
  && pecl install pdo_sqlsrv \
  && docker-php-ext-enable pdo_sqlsrv \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./php.ini /usr/local/etc/php/php.ini
