FROM php:7.1-fpm

RUN apt-get update && apt-get install -y libmcrypt-dev bash git \
    mysql-client libmagickwand-dev --no-install-recommends \
    && apt-get install -y libicu-dev\
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && git clone -b develop https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install mcrypt pdo_mysql redis gd zip\
    && sed -e 's/max_execution_time = 30/max_execution_time = 300/' -i /usr/src/php/php.ini-development \
    && sed -e 's/max_execution_time = 30/max_execution_time = 300/' -i /usr/src/php/php.ini-production \
    && sed -e 's/;request_terminate_timeout = 0/request_terminate_timeout = 300/' -i /usr/local/etc/php-fpm.d/www.conf \
    && sed -e 's/;request_terminate_timeout = 0/request_terminate_timeout = 300/' -i /usr/local/etc/php-fpm.d/www.conf.default \
    && echo "[mysqld]" >> /etc/mysql/my.cnf \
    && echo 'sql_mode = "STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"' >> /etc/mysql/my.cnf