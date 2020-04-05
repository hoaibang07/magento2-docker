FROM php:7.3.16-fpm-alpine

#Update
RUN apk update; \
    apk upgrade;

#Add required libs
RUN apk add libpng-dev; \
    apk add icu-dev
    apk add libxslt-dev
    apk add libzip-dev

#Add required php extensions
RUN docker-php-ext-install opcache gd pdo_mysql intl xsl mbstring zip bcmath soap
