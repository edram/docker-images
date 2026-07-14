FROM dunglas/frankenphp:1.9.1-php8.3-trixie

# 镜像说明
LABEL maintainer="edram"

# postgres-client 用户备份
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    ca-certificates \
    && install -d /usr/share/postgresql-common/pgdg \
    && curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail \
       https://www.postgresql.org/media/keys/ACCC4CF8.asc \
    && . /etc/os-release \
    && echo "Types: deb\n\
URIs: https://apt.postgresql.org/pub/repos/apt\n\
Suites: ${VERSION_CODENAME}-pgdg\n\
Architectures: $(dpkg --print-architecture)\n\
Components: main\n\
Signed-By: /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc" \
       > /etc/apt/sources.list.d/pgdg.sources \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
       postgresql-client-16 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

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

ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/download/2.11.1/install-php-extensions /usr/local/bin/

# imagick/imagick@master
RUN install-php-extensions \
        @composer \
        bcmath \
        intl \
        gd \
        imagick \
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
        swoole-6.0.2 \
        # laravel-medialibrary
        exif \
    ;
