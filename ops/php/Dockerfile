FROM php:5.6.40-fpm-alpine3.8

RUN apk --update --no-cache add \
        make autoconf ca-certificates php5-dev \
        zlib zlib-dev g++ dpkg libmagic file re2c \
    && sed -i 's/mozilla\/DST_Root_CA_X3.crt/!mozilla\/DST_Root_CA_X3.crt/g' /etc/ca-certificates.conf \
    && update-ca-certificates

#Redis extension
RUN curl -fsSL 'https://pecl.php.net/get/redis-4.3.0.tgz' -o /tmp/package.tgz \
    && pecl install -f /tmp/package.tgz \
	&& rm -r /tmp/package.tgz \
	&& docker-php-ext-enable redis

#XDebug extension
RUN curl -fsSL 'https://pecl.php.net/get/xdebug-2.5.5.tgz' -o /tmp/package.tgz \
    && pecl install -f /tmp/package.tgz \
	&& rm -r /tmp/package.tgz \
	&& docker-php-ext-enable xdebug

#Memcache extension
RUN curl -fsSL 'https://pecl.php.net/get/memcache-2.2.7.tgz' -o /tmp/package.tgz \
    && pecl install -f /tmp/package.tgz \
	&& rm -r /tmp/package.tgz \
	&& docker-php-ext-enable memcache

#OPCache extension
RUN  docker-php-ext-install -j$(nproc) opcache\
	&& docker-php-ext-enable opcache

#PDO's extension
RUN apk --update --no-cache add \
        freetds-dev \
    && docker-php-ext-install -j$(nproc) pdo pdo_dblib pdo_mysql \
	&& docker-php-ext-enable pdo pdo_dblib pdo_mysql

#Others extensions
RUN  docker-php-ext-install -j$(nproc) mbstring fileinfo \
	&& docker-php-ext-enable mbstring fileinfo

RUN  docker-php-ext-install -j$(nproc) mssql \
	&& docker-php-ext-enable mssql

RUN apk --update --no-cache add \
        openldap-dev \
    && docker-php-ext-install -j$(nproc) ldap \
	&& docker-php-ext-enable ldap

RUN docker-php-ext-install zip pcntl sysvmsg sysvsem \
	&& docker-php-ext-enable zip pcntl sysvmsg sysvsem

