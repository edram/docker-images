FROM edramkai/laravel:php-8.3-chrome

# 镜像说明
LABEL maintainer="edram"
LABEL version="mugroup-one"

RUN apt-get update && apt-get install -y poppler-utils \
    # 解析发票
    mupdf-tools

# postgres-client 用户备份
RUN apt-get update && apt-get install -y ca-certificates gnupg curl && rm -rf /var/lib/apt/lists/*
RUN curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |tee /etc/apt/sources.list.d/pgdg.list \
  && apt-get update && apt-get install -y postgresql-client-16

RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*