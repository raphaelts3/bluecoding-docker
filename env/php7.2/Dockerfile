FROM php:7.2-fpm

RUN apt-get update && apt-get upgrade -y
RUN apt-get update && apt-get install -y --force-yes libssl-dev curl libcurl4-gnutls-dev libxml2-dev libicu-dev libmcrypt-dev libpng-dev
RUN apt-get install -y iproute2 dnsutils

RUN docker-php-ext-install opcache
RUN docker-php-ext-install mbstring

RUN apt-get install cron -y

RUN apt-get install -y libmcrypt-dev
RUN pecl install mcrypt-1.0.1

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install soap
RUN docker-php-ext-install gd

RUN pecl install redis
RUN pecl install xdebug

RUN echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

RUN echo "zend_extension=xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_autostart=1" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_mode=req" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_host=`/sbin/ip route|awk '/default/ { print $3 }'`" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.profiler_enable=0" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_log=/app/log/xdebug.log" >> /usr/local/etc/php/conf.d/xdebug.ini

CMD ["php-fpm"]