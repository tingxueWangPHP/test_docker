FROM gcc:4.9 as builder

ARG exe=mytest

RUN mkdir /data

COPY ./1.c /data

WORKDIR /data

RUN gcc -o ${exe} 1.c

FROM php:7.4-fpm

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups

WORKDIR /var/www/html

COPY --from=builder /data/${exe} ../

RUN ../mytest

EXPOSE 9000

ENV PATH=/home:$PATH
