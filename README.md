# Laravel Docker

### It is similar to Sail but limitation and hard to use more.

- PHP 8.1
- MariaDB 10.8
- phpmyadmin:latest
- phpRedisAdmin:latest
- redis:alpine
- Laravel latest

## Setup
- ``docker-compose up -d``
- ``docker exec -it php_ctn_name /bin/bash``
- ``cp .env.live .env``
- ``composer update``
- ``chmod -R gu+w storage/ && chmod -R guo+w storage/ && chmod -R gu+w bootstrap/cache/ && chmod -R guo+w bootstrap/cache/``
- ``service cron start`` if need run Schedule
- ``exit``
