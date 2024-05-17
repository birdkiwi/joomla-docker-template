FROM php:8.3.1-fpm

WORKDIR /var/www/html

RUN sed -i 's/http:x:[[:digit:]]\+:http/http:x:'${LOCAL_GROUP_ID}':http/g' /etc/group && cat /etc/group
RUN sed -i 's/http:x:[[:digit:]]\+:[[:digit:]]\+:/http:x:'${LOCAL_USER_ID}':'${LOCAL_GROUP_ID}':/g' /etc/passwd && cat /etc/passwd
RUN echo 'root:Docker!' | chpasswd

RUN apt-get update && apt-get install -y \
        libzip-dev \
        zip \
		libfreetype-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
        libicu-dev \
        libwebp-dev \
        libavif-dev

RUN docker-php-ext-configure zip
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp --with-avif
RUN docker-php-ext-configure intl

RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN docker-php-ext-install zip
RUN docker-php-ext-install intl

RUN docker-php-ext-enable mysqli
