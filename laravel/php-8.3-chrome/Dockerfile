FROM edramkai/laravel:php-8.3

# 镜像说明
LABEL maintainer="edram"
LABEL version="php-8.3-chrome"

RUN apt-get update && apt-get install -y wget

RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get install -y --fix-missing ./google-chrome-stable_current_amd64.deb \
    && rm -rf ./google-chrome-stable_current_amd64.deb

RUN wget https://packages.microsoft.com/repos/edge/pool/main/m/microsoft-edge-stable/microsoft-edge-stable_130.0.2849.68-1_amd64.deb \
    && apt-get install -y --fix-missing ./microsoft-edge-stable_130.0.2849.68-1_amd64.deb \
    && rm -rf ./microsoft-edge-stable_130.0.2849.68-1_amd64.deb

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - 
RUN apt-get install -y nodejs
RUN corepack enable pnpm

RUN npm install -g puppeteer

RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*