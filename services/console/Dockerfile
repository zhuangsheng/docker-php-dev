 
FROM php:7.0
MAINTAINER zhuangsheng

WORKDIR /code

# 常用工具
RUN apt-get update && apt-get install -y git curl wget cron vim locales libfreetype6-dev mariadb-client \
  && rm -rf /var/lib/apt/lists/* \
  && pecl install zip \
  && docker-php-ext-enable zip \
  && docker-php-ext-install mysqli pdo_mysql

# 把语言设置成简体中文
RUN dpkg-reconfigure locales && \
  locale-gen C.UTF-8 && \
  /usr/sbin/update-locale LANG=C.UTF-8
RUN echo 'zh_CN.UTF-8 UTF-8' >> /etc/locale.gen && \
  locale-gen
ENV LC_ALL C.UTF-8
ENV LANG zh_CN.UTF-8
ENV LANGUAGE zh_CN.UTF-8

# 配置 git
RUN git config --global user.name "zhuangsheng" \
  && git config --global user.email "zhuang3c@gmail.com"

# 安装与配置 composer
# Composer 官方安装脚本 https://getcomposer.org/download/1.2.1/composer.phar
# 
ENV COMPOSER_VERSION 1.2.1
COPY ./composer-$COMPOSER_VERSION.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc \
  && . ~/.bashrc \
  && composer config -g repo.packagist composer https://packagist.phpcomposer.com

