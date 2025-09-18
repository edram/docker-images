FROM dunglas/frankenphp:1.9.1-php8.4-bookworm

# 镜像说明
LABEL maintainer="edram"

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