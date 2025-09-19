FROM edramkai/laravel:php-8.3-chrome

# 镜像说明
LABEL maintainer="edram"
LABEL version="mugroup-one"

RUN apt-get update && apt-get install -y poppler-utils \
    # 解析发票
    mupdf-tools

# postgres-client 用户备份
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl ca-certificates gnupg lsb-release && \
    install -d /usr/share/postgresql-common/pgdg && \
    curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc && \
    echo "deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" \
        > /etc/apt/sources.list.d/pgdg.list && \
    apt-get -y install postgresql-client-16

RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*