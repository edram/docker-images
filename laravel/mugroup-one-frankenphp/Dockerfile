FROM dunglas/frankenphp:1.9.1-php8.3-bookworm

# 镜像说明
LABEL maintainer="edram"

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y ca-certificates gnupg lsb-release curl && rm -rf /var/lib/apt/lists/*

# postgres-client 用户备份
RUN curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |tee /etc/apt/sources.list.d/pgdg.list \
  && apt-get update && apt-get install -y postgresql-client-16

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
        # pdf
        poppler-utils \ 
        # 解析发票
        mupdf-tools \
    # 清理镜像
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - 
RUN apt-get install -y nodejs
RUN corepack enable pnpm

RUN npm install -g puppeteer

RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get install -y --fix-missing ./google-chrome-stable_current_amd64.deb \
    && rm -rf ./google-chrome-stable_current_amd64.deb

RUN install-php-extensions \
        @composer \
        bcmath \
        intl \
        gd \
        imagick/imagick@master \
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