FROM alpine:3.7

# trust this project public key to trust the packages.
ADD https://php.codecasts.rocks/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub

RUN set -xe \
    && echo "@php https://php.codecasts.rocks/v3.7/php-7.2" >> /etc/apk/repositories \
    && apk add --update --no-cache \
    ca-certificates \
    curl \
    nano \
    nginx \
    git \
    supervisor \
    php7@php \
    php7-curl@php \
    php7-fpm@php \
    php7-gd@php \
    php7-intl@php \
    php7-mbstring@php \
    php7-pdo@php \
    php7-zip@php \
    php7-xml@php \
    php7-pdo_mysql@php \
    php7-json@php \
    php7-phar@php \
    php7-openssl@php \
    php7-zlib@php \
    php7-ctype@php \
    php7-dom@php \ 
    php7-session@php \
    php7-iconv@php \
    nodejs \
    yarn \
    openssh-client \
    rsync

RUN set -x \
    && ln -s /usr/bin/php7 /usr/bin/php \
    && adduser -u 82 -D -S -G www-data www-data

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY php.ini /etc/php7/conf.d/50-setting.ini
COPY pool.conf /etc/php7/php-fpm.d/www.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY supervisord.conf /etc/supervisord.conf

EXPOSE 80
WORKDIR /app

CMD ["supervisord", "-c", "/etc/supervisord.conf"]
