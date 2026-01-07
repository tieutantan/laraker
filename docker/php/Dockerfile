FROM php:8.4-fpm-alpine

# ========= System dependencies =========
RUN apk add --no-cache \
    bash \
    git \
    curl \
    zip \
    unzip \
    supervisor \
    icu-dev \
    oniguruma-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    autoconf \
    gcc \
    g++ \
    make \
    linux-headers

# ========= PHP extensions =========
RUN docker-php-ext-configure gd \
        --with-freetype \
        --with-jpeg \
    && docker-php-ext-install \
        bcmath \
        pdo \
        pdo_mysql \
        mbstring \
        intl \
        zip \
        exif \
        gd \
        opcache

# ========= Xdebug =========
RUN pecl install xdebug && docker-php-ext-enable xdebug

# ========= Redis =========
RUN pecl install redis && docker-php-ext-enable redis

# ========= Composer =========
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# ========= PHP config =========
COPY docker/php/php.ini /usr/local/etc/php/conf.d/custom.ini
COPY docker/php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# ========= Supervisor =========
RUN mkdir -p /var/log/supervisor /var/run
COPY docker/php/supervisor.conf /etc/supervisord.conf

WORKDIR /var/www

CMD ["supervisord", "-c", "/etc/supervisord.conf", "-n"]
