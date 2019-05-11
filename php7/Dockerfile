FROM php:7.1-fpm-alpine

MAINTAINER ZxKill

RUN apk add --update \
            freetype \
            gd \
            libpng \
            libjpeg-turbo \
            freetype-dev \
            libpng-dev \
            jpeg-dev \
            libjpeg \
            libjpeg-turbo-dev \
            libmcrypt-dev \
            curl \
            wget \
            git \
            msmtp\
            re2c \
 && docker-php-ext-configure gd \
            --with-freetype-dir=/usr/lib/ \
            --with-png-dir=/usr/lib/ \
            --with-jpeg-dir=/usr/lib/ \
            --with-gd \
 && docker-php-ext-install -j$(nproc) \
            iconv \
            zip \
            mysqli \
            pdo \
            pdo_mysql \
            gd \
            bcmath \
            session \
            opcache \
            mcrypt

RUN apk add autoconf g++ libtool make

RUN  wget -O memcache.tgz https://codeload.github.com/websupport-sk/pecl-memcache/tar.gz/4.0.3?dummy=/ \
     && gunzip memcache.tgz \
     && tar -xvf memcache.tar \
     && cd pecl-memcache-4.0.3 \
     && phpize \
     && ./configure && make && make install \
     && cd && rm -rf pecl-memcache-4.0.3
     #&& pecl install xdebug \

RUN docker-php-ext-enable memcache

RUN apk add composer

# MSMTP
ADD msmtprc /etc/msmtprc
RUN chmod 0600 /etc/msmtprc && \
    chown www-data:www-data /etc/msmtprc && \
    mkdir -p /var/log/msmtp/msmtp.log && \
    touch /var/log/msmtp/msmtp.log && \
    chmod 775 /var/log/msmtp/msmtp.log && \
    chown www-data:www-data /var/log/msmtp/msmtp.log

RUN rm -rf /var/cache/apk/*

WORKDIR "/var/www/bitrix"

EXPOSE 9000

CMD ["php-fpm"]