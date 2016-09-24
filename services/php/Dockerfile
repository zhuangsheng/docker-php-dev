FROM php:7.0-fpm
MAINTAINER zhuang3c@gmail.com

RUN mkdir -p /usr/src/php/ext

ENV PHPREDIS_VERSION 3.0.0
RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
 && tar xfz /tmp/redis.tar.gz \
 && rm -r /tmp/redis.tar.gz \
 && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis

ENV PHPYAF_VERSION yaf-3.0.4
RUN curl -L -o /tmp/yaf.tar.gz https://github.com/laruence/yaf/archive/$PHPYAF_VERSION.tar.gz \
 && tar xfz /tmp/yaf.tar.gz \
 && rm -r /tmp/yaf.tar.gz \
 && mv yaf-$PHPYAF_VERSION /usr/src/php/ext/yaf

RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev \
  && rm -rf /var/lib/apt/lists/* \
  && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
  && docker-php-ext-install gd mysqli pdo_mysql zip redis yaf

COPY ./config/php.ini /usr/local/etc/php/conf.d/
COPY ./config/yaf.ini /usr/local/etc/php/conf.d/

