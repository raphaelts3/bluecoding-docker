FROM php:7.2-fpm

RUN apt-get update && apt-get upgrade -y
RUN apt-get update && apt-get install -y \
    --allow-downgrades --allow-remove-essential --allow-change-held-packages \
    libssl-dev curl libcurl4-gnutls-dev libxml2-dev libicu-dev libmcrypt-dev \
    libpng-dev git zip unzip iproute2 dnsutils cron libmcrypt-dev zip unzip

RUN pecl install mcrypt-1.0.1
RUN pecl install redis
RUN pecl install xdebug

RUN docker-php-ext-install opcache
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install soap
RUN docker-php-ext-install gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

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

CMD ["php-fpm"]