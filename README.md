# Laraker

- PHP 8.3, xDebug 3.3.1 Build
- MariaDB 11.2
- phpmyadmin:latest
- phpRedisAdmin:latest
- redis:alpine
- Auto clear access log, error log.

## Setup
- `git clone https://github.com/tieutantan/Laraker.git`
- Install Docker ``./install_docker.sh`` * Optional
- ``docker-compose up -d``

## Commands

- `docker exec -it laraker-php83 /bin/bash`
- `service cron status`
- `service cron start`
- `service cron stop`
