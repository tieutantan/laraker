# Laraker

Laraker is a Docker-based local development environment for PHP (Laravel-ready), Node.js, MySQL, Redis, and supporting tools. It provides a pre-configured stack for rapid development and debugging.

## Features
- PHP 8.4 (FPM, Alpine) with Xdebug and Redis extensions
- Node.js 24 (for frontend asset building)
- Nginx 1.27 (serves app on port 8001)
- MySQL 8.0 (port 3306, persistent storage)
- Redis 7.4 (port 6379, persistent storage)
- Supervisor (manages PHP-FPM, Laravel queue, and scheduler)
- Custom PHP and Xdebug configuration
- Auto-build Node.js assets on container start

## Prerequisites
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/)

## Setup
1. Clone the repository:
   ```sh
   git clone https://github.com/tieutantan/Laraker.git
   cd Laraker
   ```
2. (Optional, Ubuntu only) Install Docker & Docker Compose:
   ```sh
   ./install_docker.sh
   ```
3. Start the containers:
   ```sh
   docker-compose up -d
   ```
4. Access your app at: [http://localhost:8001](http://localhost:8001)

## Service Details
- **PHP**: 8.4 FPM, with Xdebug and Redis extensions, Composer installed
- **Node.js**: 24, auto-builds assets on start
- **Nginx**: Serves `/src/public` on port 8001
- **MySQL**: 8.0, port 3306
  - Database: `laraker_db`
  - User: `user1`, Password: `user1pw123456`
  - Root Password: `rootp@pwroot1`
- **Redis**: 7.4, port 6379
- **Supervisor**: Runs PHP-FPM, Laravel queue, and scheduler

## Usage
- Enter PHP container:
  ```sh
  docker exec -it laraker-app /bin/bash
  ```
- Laravel queue worker and scheduler are managed by Supervisor (see `docker/php/supervisor.conf`).
- Xdebug is enabled and configurable via environment variables in `docker/php/xdebug.ini`.
- Custom PHP settings in `docker/php/php.ini`.
- MySQL and Redis data are persisted via Docker volumes.

## Notes
- Place your Laravel project in the `src` directory. The web root is `src/public`.
- Node.js assets are built automatically on container start. Adjust the build command in `docker-compose.yml` if needed.
- To change PHP or Xdebug settings, edit the corresponding files in `docker/php/` and restart the containers.

## Troubleshooting
- If you encounter permission issues, ensure Docker has access to your project directory.
- For Xdebug remote debugging, set `XDEBUG_CLIENT_HOST` and `XDEBUG_MODE` as needed.
- To stop all containers:
  ```sh
  docker-compose down
  ```

## Credits
- Inspired by Laravel, Docker, and community best practices.

---

*Note: phpMyAdmin and phpRedisAdmin are not included by default. Add them to `docker-compose.yml` if needed.*
