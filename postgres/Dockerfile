FROM postgres:11.5-alpine

# Копируем словари для поиска
COPY ./tsearch_data /usr/local/share/postgresql/tsearch_data

# Устаналиваем сторонний парсер для поиска
ADD https://github.com/postgrespro/pg_tsparser/archive/master.zip /home

RUN apk add --no-cache --virtual .build-deps \
		gcc \
    make \
    libc-dev \
    icu-dev \
    && cd /home \
    && unzip master.zip \
    && rm -rf master.zip \
    && cd pg_tsparser-master \
    && make USE_PGXS=1 install \
    && rm -rf /home/pg_tsparser-master \
    && apk del .build-deps
