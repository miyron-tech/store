FROM php:8.1-fpm-alpine

COPY php.ini /usr/local/etc/php/conf.d/docker-fpm.ini

RUN apk update \
    apk add git \
    apk add postgresql-dev \ 
    docker-php-ext-install pdo pdo_pgsql \
    docker-php-ext-enable pdo_pgsql

#composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \ 
    && mv composer.phar /usr/local/bin/composer

WORKDIR /var/www/app