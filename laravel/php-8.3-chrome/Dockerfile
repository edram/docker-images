FROM edramkai/laravel:php-8.3

# 镜像说明
LABEL maintainer="edram"
LABEL version="php-8.3-chrome"

RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg \
    && install -o root -g root -m 644 microsoft.gpg /usr/share/keyrings/ \
    && sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/edge stable main" > /etc/apt/sources.list.d/microsoft-edge-beta.list' \
    && rm microsoft.gpg \
    && apt update \
    && apt install microsoft-edge-beta

RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    apt install --fix-missing ./google-chrome-stable_current_amd64.deb

RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*