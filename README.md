# Overview
Simple Laravel environment by Docker and Docker-compose.

Ref by...
https://reffect.co.jp/laravel/finally-understand-laravel-on-docker#MySQL-2


# How to...
## Start Dcoker
docker-compose up -d

**It must be executed at first.**

## Install laravel by composer
docker run --rm -v {Current Directly}/src:/app composer create-project --prefer-dist laravel/laravel .

## ~composer update~
~docker run --rm -v {Current Directly}/src:/app composer update (install?)~

## Make .env file
DB_CONNECTION=mysql

DB_HOST=mysql

DB_PORT=3306

DB_DATABASE=laravel

DB_USERNAME=root

DB_PASSWORD=password

## Create encryption key (It may be not needed)
docker-compose exec php php artisan key:generate

-> Write down automatically `APP_KEY`

## Top page
http://127.0.0.1:8080/


# Ohter
## laravel/ui package
docker run --rm -v {Current Directly}/src:/app composer require laravel/ui

docker exec -it php php artisan ui vue --auth

docker run --rm -v {Current Directly}/src:/usr/src/app -w /usr/src/app node npm install && npm run dev

docker-compose exec php php artisan migrate

# 課題
## src and db
最初からデータ入りにすべきか、なしにすべきか…今のDockercompose.ymlで冪等性を保てるようにしたい。

## src
データ有: composer updateでvendor等の再ダウンロードが必要。 
データ無:

## db
### データ有
データベース名の変更ができない。ファイル名の変更でできる？
### データ無
dbコンテナの起動を行う際に、docker-compose.ymlのmysqlに
```
user: "1000:50"
```
を入れないと正しく起動できない。
