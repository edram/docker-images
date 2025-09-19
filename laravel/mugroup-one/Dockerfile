FROM edramkai/laravel:php-8.3-chrome

# 镜像说明
LABEL maintainer="edram"
LABEL version="mugroup-one"

RUN apt-get update && apt-get install -y poppler-utils \
    # 解析发票
    mupdf-tools

# postgres-client 用户备份
RUN apt-get update && \
    apt-get install -y curl ca-certificates && install -d /usr/share/postgresql-common/pgdg && curl -o /usr/share/postgresql-common pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc && . /etc/os-release && sh -c "echo 'deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $VERSION_CODENAME-pgdg main' > /etc/apt/sources.list.d/pgdg.list" && \
    apt-get update && \
    apt-get -y install postgresql-client-16

RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*