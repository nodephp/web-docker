FROM php:7.3-fpm-stretch
MAINTAINER forfire "forfire@foxmail.com"
# 设置时区
COPY aliyun.list /etc/apt/
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    cp /etc/apt/sources.list /etc/apt/bak.list && mv /etc/apt/aliyun.list /etc/apt/sources.list && apt-get update 
RUN apt-get install -y \
        procps \
        vim \
        bash-completion \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
        && docker-php-ext-install zip \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install opcache \
        && docker-php-ext-install mysqli \
        && rm -r /var/lib/apt/lists/*

COPY ./pkg/* /home/

# 安装 PECL 拓展
RUN pecl install /home/redis.tgz \
    && pecl install /home/yaf.tgz  \
    && rm -f /home/redis.tgz  /home/yaf.tar.gz  /usr/local/etc/php/conf.d/*
# 安装 Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

RUN usermod -u 1000 www-data && mkdir -p /data/logs/php && mkdir -p /data/logs/app  && mkdir -p /data/wwwroot && chown -R www-data:www-data /data
WORKDIR /data