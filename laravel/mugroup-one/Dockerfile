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

# https://pptr.dev/troubleshooting#chrome-doesnt-launch-on-linux
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        fonts-liberation \
        libasound2 \
        libatk-bridge2.0-0 \
        libatk1.0-0 \
        libatspi2.0-0 \
        libc6 \
        libcairo2 \
        libcups2 \
        libdbus-1-3 \
        libdrm2 \
        libexpat1 \
        libfontconfig1 \
        libgbm1 \
        libgcc1 \
        libglib2.0-0 \
        libgtk-3-0 \
        libnspr4 \
        libnss3 \
        libpango-1.0-0 \
        libpangocairo-1.0-0 \
        libstdc++6 \
        libx11-6 \
        libx11-xcb1 \
        libxcb1 \
        libxcomposite1 \
        libxcursor1 \
        libxdamage1 \
        libxext6 \
        libxfixes3 \
        libxi6 \
        libxkbcommon0 \
        libxrandr2 \
        libxrender1 \
        libxshmfence1 \
        libxss1 \
        libxtst6 \
        lsb-release \
        wget \
        xdg-utils \
    && rm -rf /var/lib/apt/lists/*

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
