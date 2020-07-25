# Overview
Simple Laravel environment by Docker and Docker-compose.

Ref by...
https://reffect.co.jp/laravel/finally-understand-laravel-on-docker#MySQL-2

# How to...
## composer update
docker run --rm -v /mnt/c/Users/miura/program/env_laravel-docker/src:/app composer update (install?)
## Make .env file
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=password
## Create encryption key
docker-compose exec php php artisan key:generate
-> Write down automatically `APP_KEY`

# laravel/ui package
docker run --rm -v /mnt/c/Users/miura/program/env_laravel-docker/src:/app composer require laravel/ui
docker exec -it php php artisan ui vue --auth
docker run --rm -v /mnt/c/Users/miura/program/env_laravel-docker/src:/usr/src/app -w /usr/src/app node npm install && npm run dev
docker-compose exec php php artisan migrate
