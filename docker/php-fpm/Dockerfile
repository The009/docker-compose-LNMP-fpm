FROM php:8.5.0-fpm
WORKDIR "/app"

# Update
RUN apt-get update

# Install ZIP
RUN apt-get install -y libzip-dev zip

# Install PHP extensions
RUN docker-php-ext-install zip pdo pdo_mysql mysqli

# Install Redis
RUN pecl install -o -f redis && docker-php-ext-enable redis

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN apt-get update && apt-get install -y wget \
    && wget https://xdebug.org/files/xdebug-3.5.0.tgz \
    && tar -xvzf xdebug-3.5.0.tgz \
    && cd xdebug-3.5.0 \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && docker-php-ext-enable xdebug \
    && cd .. \
    && rm -rf xdebug-3.5.0 xdebug-3.5.0.tgz

# Cleanup
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
