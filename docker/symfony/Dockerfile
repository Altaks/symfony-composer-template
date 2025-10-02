FROM php:fpm-alpine3.22

# Login to container as root user
USER root

# Symfony dev environement
ENV APP_ENV=dev

# Copy php default configuration
COPY ./docker/symfony/default.ini /usr/local/etc/php/conf.d/default.ini

# Set working directory
WORKDIR /app

# Installer XDebug
RUN apk add linux-headers
RUN apk add bash git $PHPIZE_DEPS
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Modules pour utiliser MySQL
RUN docker-php-ext-install mysqli pdo_mysql

# Installer composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

# Installer la CLI Symfony
RUN apk add --no-cache bash
RUN curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.alpine.sh' | bash
RUN apk add symfony-cli

# Arguments defined in compose.yml
ARG USER_NAME
ARG USER_ID
ARG GROUP_NAME
ARG GROUP_ID

# Create system user to run Composer and PHP Commands
RUN if [ ! -z ${USER_NAME} ] && [ ! -z ${GROUP_NAME} ] && [ ${USER_ID:-0} -ne 0 ] && [ ${GROUP_ID:-0} -ne 0 ] ; then \
    addgroup ${GROUP_NAME} && \
    adduser -G www-data -G root -G ${GROUP_NAME} -u $USER_ID -h /home/$USER_NAME -D $USER_NAME && \
    mkdir -p /home/$USER_NAME/.composer  && \
    chown -Rf ${USER_NAME}:${GROUP_NAME} /home/$USER_NAME  && \
    chown -R ${USER_NAME}:${GROUP_NAME} /app \
    ; fi

# Login to container as non-root user
USER ${USER_ID:-0}:${GROUP_ID:-0}