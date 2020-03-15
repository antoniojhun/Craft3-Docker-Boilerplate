FROM php:7.3-fpm

# Install libraries
RUN apt-get update && apt-get install -y \
    libfreetype6-dev libjpeg62-turbo-dev libpq-dev \
    libpng-dev libbz2-dev libcurl3-dev \
    gcc make libc-dev pkg-config zlib1g-dev \
    libssl-dev libmemcached-dev autoconf memcached \
    ca-certificates curl g++ libicu-dev \
    libmagickwand-dev mariadb-client libzip-dev \
    && \
    pecl install \
    apcu \
    imagick-3.4.3 \
    xdebug \
    memcached && \
    docker-php-ext-install \
    bcmath bz2 exif \
    ftp gd gettext mbstring opcache \
    shmop sockets sysvmsg sysvsem sysvshm \
    zip iconv pdo_mysql intl && \
    docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-enable imagick && \
    docker-php-ext-enable apcu && \
    docker-php-ext-enable memcached && \
    docker-php-ext-configure bcmath && \
    docker-php-ext-install \
    soap \
    zip \
    curl \
    bcmath \
    exif \
    gd \
    iconv \
    intl \
    mbstring \
    opcache \
    pdo_mysql \
    pdo_pgsql

# Configure version constraints
ENV VERSION_COMPOSER_ASSET_PLUGIN=^1.4.6 \
    VERSION_PRESTISSIMO_PLUGIN=^0.3.10 \
    PATH=/app:/app/vendor/bin:/root/.composer/vendor/bin:$PATH \
    TERM=linux \
    COMPOSER_ALLOW_SUPERUSER=1


# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin/ --filename=composer && \
    composer global require --optimize-autoloader \
    "fxp/composer-asset-plugin:${VERSION_COMPOSER_ASSET_PLUGIN}" \
    "hirak/prestissimo:${VERSION_PRESTISSIMO_PLUGIN}" && \
    composer global dumpautoload --optimize && \
    composer clear-cache

# Set PHP ini configuration
RUN echo "date.timezone ="Australia/Brisbane" " > /usr/local/etc/php/php.ini && \
    echo "upload_max_filesize = 100M" > /usr/local/etc/php/php.ini && \    
    echo "post_max_size = 100M" >> /usr/local/etc/php/php.ini && \
    echo "max_execution_time = 500" >> /usr/local/etc/php/php.ini && \
    echo "memory_limit = 256M" >> /usr/local/etc/php/php.ini && \
    echo "; Security, Debug & Logs" >> /usr/local/etc/php/php.ini && \
    echo "expose_php = off" >> /usr/local/etc/php/php.ini && \
    echo "cgi.fix_pathinfo = 0" >> /usr/local/etc/php/php.ini && \
    echo "error_reporting = E_ALL" >> /usr/local/etc/php/php.ini && \
    echo "html_errors = on" >> /usr/local/etc/php/php.ini && \
    echo "xdebug.default_enable = off" >> /usr/local/etc/php/php.ini && \
    echo "; Opcache" >> /usr/local/etc/php/php.ini && \
    echo "opcache.revalidate_freq = 0" >> /usr/local/etc/php/php.ini && \
    echo "opcache.validate_timestamps = \${PHP_REVALIDATE}" >> /usr/local/etc/php/php.ini && \
    echo "opcache.memory_consumption = 128" >> /usr/local/etc/php/php.ini && \
    echo "opcache.interned_strings_buffer = 8" >> /usr/local/etc/php/php.ini && \
    echo "opcache.max_accelerated_files = 4000" >> /usr/local/etc/php/php.ini && \
    echo "opcache.fast_shutdown = 0" >> /usr/local/etc/php/php.ini && \
    echo "opcache.enable_cli = 1" >> /usr/local/etc/php/php.ini

# Copy our project into the container and install dependencies
COPY --chown=www-data:www-data ./src /var/www/html

RUN composer install -d /var/www/html/ && \
    chown -R www-data:www-data /var/www/html/vendor && \
    chown -R www-data:www-data /var/www/html/composer.lock

COPY ./docker-containers/php/zzz-docker.conf /usr/local/etc/php-fpm.d/zzz-docker.conf