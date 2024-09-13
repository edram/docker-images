FROM php:7.3.32-cli-bullseye

# 镜像说明
LABEL maintainer="edram"
LABEL version="php-7.3.32"

# 配置阿里云镜像
# RUN echo 'http://mirrors.aliyun.com/alpine/v3.14/main/' > /etc/apk/repositories \
#     && echo 'http://mirrors.aliyun.com/alpine/v3.14/community/' >> /etc/apk/repositories

# composer
RUN curl https://github.com/composer/composer/releases/download/2.0.14/composer.phar -s -S -o /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer
ENV PATH=/root/.composer/vendor/bin:$PATH

# 安装额外依赖
RUN apt-get update \
    && apt-get -y install \
        # composer install 需要解压
        unzip \
        # 提供 cron 定时任务
        cron \
        # supervisor
        supervisor \
    # 清理镜像
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# php
ADD https://github.com/mlocati/docker-php-extension-installer/releases/download/2.5.0/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions \
        bcmath \
        gd \
        # mysql
        mysqli pdo_mysql \
        # sqlsrv
        sqlsrv pdo_sqlsrv \
        # maatwebsite/excel
        zip \
        # queue
        pcntl \
        # redis
        redis \ 
        # swoole
        swoole \
        # laravel-medialibrary
        exif \
    ;