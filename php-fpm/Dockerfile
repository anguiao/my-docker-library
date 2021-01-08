FROM php:7.4.14-fpm-alpine

ENV TZ=Asia/Shanghai

RUN apk update \
	&& apk add tzdata \
	&& echo "${TZ}" > /etc/timezone \
	&& ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
	\
	&& docker-php-ext-install -j$(nproc) pdo_mysql \
	\
	&& apk add \
		freetype \
		freetype-dev \
		libjpeg-turbo \
		libjpeg-turbo-dev \
	&& docker-php-ext-configure gd \
		--with-freetype=/usr/include/ \
		--with-jpeg=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& apk del \
		freetype-dev \
		libjpeg-turbo-dev \
	\
	&& rm /var/cache/apk/*

COPY ./php.ini /usr/local/etc/php/
COPY ./www.conf /usr/local/etc/php-fpm.d/
