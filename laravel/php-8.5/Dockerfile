FROM dunglas/frankenphp:1.12.4-php8.5-trixie

# 镜像说明
LABEL maintainer="edram"

# 安装额外依赖
RUN apt-get update \
    && apt-get -y install \
        wget \
        # composer install 需要解压
        unzip \
        # 提供 cron 定时任务
        cron \
        # supervisor
        supervisor \
        # image
        jpegoptim \
        optipng pngquant \
    # 清理镜像
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

ENV COMPOSER_HOME=/root/.composer
ENV PATH="${COMPOSER_HOME}/vendor/bin:${PATH}"

RUN install-php-extensions \
        @composer \
        bcmath \
        intl \
        gd \
        imagick \
        # mysql
        mysqli pdo_mysql \
        # maatwebsite/excel
        zip \
        # queue
        pcntl \
        # redis
        redis \ 
        # laravel-medialibrary
        exif \
    ;

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_24.x | bash - 
RUN apt-get install -y nodejs \
    && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN corepack enable pnpm