FROM edramkai/laravel:php-8.3

# 镜像说明
LABEL maintainer="edram"
LABEL version="php-8.3-chrome"

RUN apt-get update && apt-get install -y wget

RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get install -y --fix-missing ./google-chrome-stable_current_amd64.deb \
    && rm -rf ./google-chrome-stable_current_amd64.deb

RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*