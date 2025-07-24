FROM edramkai/laravel:php-8.3-chrome

# 镜像说明
LABEL maintainer="edram"
LABEL version="mugroup-one"

RUN apt-get update && apt-get install -y poppler-utils \
    # 解析发票
    mupdf-tools

RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*