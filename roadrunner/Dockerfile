FROM spiralscout/roadrunner:2.0.4 as rr

FROM php:8.0-cli-alpine3.12 as php

RUN apk update && apk add --no-cache \
  vim \
  libzip-dev \
  unzip \
  openssl \
  curl

RUN docker-php-ext-install zip \
  && docker-php-ext-install sockets \
  && docker-php-ext-install opcache \
  && docker-php-ext-enable opcache

COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY --from=rr /usr/bin/rr /usr/bin/rr

COPY --from=rr /etc/rr.yaml /etc/rr.yaml

CMD ["/usr/bin/rr", "serve", "-d", "-c", "/etc/rr.yaml"]
