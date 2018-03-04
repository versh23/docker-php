FROM ubuntu:16.04

ENV  LANG="en_US.UTF-8" \
     LC_ALL="en_US.UTF-8" \
     LANGUAGE="en_US.UTF-8" \
     TERM="xterm" \
     DEBIAN_FRONTEND="noninteractive" \
     COMPOSER_ALLOW_SUPERUSER=1

EXPOSE 80
WORKDIR /app

RUN apt-get update -q && \
    apt-get install -qy software-properties-common language-pack-en-base && \
    export LC_ALL=en_US.UTF-8 && \
    export LANG=en_US.UTF-8 && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update -q && \
    apt-get install --no-install-recommends -qy \
        ca-certificates \
        curl \
        nano \
        nginx \
        git \
        php7.2 \
        php7.2-curl \
        php7.2-fpm \
        php7.2-gd \
        php7.2-intl \
        php7.2-mbstring \
        php7.2-pdo \
        php7.2-zip \
        php7.2-xml \
        php7.2-mysql \
        supervisor && \

    mkdir /run/php && \

    cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime && echo "Europe/Moscow" > /etc/timezone && \

    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \

    curl -sL https://deb.nodesource.com/setup_8.x | bash && apt-get install -y nodejs && \

    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update -q && apt-get install --no-install-recommends -qy yarn && \

    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY php.ini /etc/php/7.2/cli/conf.d/50-setting.ini
COPY php.ini /etc/php/7.2/fpm/conf.d/50-setting.ini
COPY pool.conf /etc/php/7.2/fpm/pool.d/www.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]