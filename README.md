# Overview
Simple Laravel environment by Docker and Docker-compose.

Ref by...
https://reffect.co.jp/laravel/finally-understand-laravel-on-docker#MySQL-2


# How to...
## Start Dcoker
docker-compose up -d

**It must be executed at first.**

## Change DB name
If you want to change DB name, you need to change change 'docker-compose.yml'.
```
environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: lara_db # Here!!
```

## Install laravel by composer
docker run --rm -v {Current Directly}/src:/app composer create-project --prefer-dist laravel/laravel .

## composer update (If already installed)
docker run --rm -v {Current Directly}/src:/app composer update (install?)

## Make .env file
```
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel # Set DB name
DB_USERNAME=root
DB_PASSWORD=password
```

## Create encryption key (It may be not needed)
docker-compose exec php php artisan key:generate

-> Write down automatically `APP_KEY`

## Fail to download files in db (It may be not needed)
Add this code under mysql in `docker-compose.yml`.
```
depends_on:
      -  php
      -  mysql
user: "1000:50" # Here!!
```

## Top page
http://127.0.0.1:8080/


# Ohter
## laravel/ui package
```
docker run --rm -v {Current Directly}/src:/app composer require laravel/ui
docker exec -it php php artisan ui vue --auth
docker run --rm -v {Current Directly}/src:/usr/src/app -w /usr/src/app node npm install && npm run dev
docker-compose exec php php artisan migrate
```

# Issue
## Too slow and ideas of sollution
It is because of WSL2. Not to use WSL2, then it was improved.
https://stackoverflow.com/questions/63036490/docker-is-extremely-slow-when-running-laravel-on-nginx-container-wsl2

### Other ideas to improve.
Reduce mount files.
https://qiita.com/ProjectEuropa/items/c094cfb4aac2968a9901

Use docker-sync.
https://qiita.com/reflet/items/ee15bf6b1b90a3a90905

https://qiita.com/miyawa-tarou/items/7ffdd8af86c57ca80ed1
