FROM php:5.6-fpm-alpine
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
	&& apk update \
	&& apk add --no-cache openssl-dev libxml2-dev libpng-dev libjpeg-turbo-dev freetype-dev \
	&& docker-php-ext-install -j$(nproc) mysqli pdo_mysql bcmath soap zip \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& apk add --no-cache --virtual .build-deps autoconf dpkg-dev dpkg file g++ gcc libc-dev make pkgconf re2c \
	&& pecl install xdebug-2.5.5 \
	&& pecl install redis-4.3.0 \
	&& pecl install mongodb-1.5.5 \
	&& pecl install mongo-1.6.16 \
	&& docker-php-ext-enable redis mongodb mongo \
	&& apk del .build-deps \
    && rm -rf /tmp/*