FROM dunglas/frankenphp:1.9.1-php8.4-bookworm

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
        # pdf
        poppler-utils \ 
        # 解析发票
        mupdf-tools \
    # 清理镜像
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# 浏览器 https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get install -y --fix-missing ./google-chrome-stable_current_amd64.deb \
    && rm -rf ./google-chrome-stable_current_amd64.deb

RUN wget https://packages.microsoft.com/repos/edge/pool/main/m/microsoft-edge-stable/microsoft-edge-stable_133.0.3065.92-1_amd64.deb \
    && apt-get install -y --fix-missing ./microsoft-edge-stable_133.0.3065.92-1_amd64.deb \
    && rm -rf ./microsoft-edge-stable_133.0.3065.92-1_amd64.deb

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - 
RUN apt-get install -y nodejs
RUN corepack enable pnpm

RUN npm install -g puppeteer

RUN install-php-extensions \
        bcmath \
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