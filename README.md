# django-on-docker

testdriven.ioの[Dockerizing Django with Postgres, Gunicorn, and Nginx](https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/)を写経したリポジトリ

## 起動方法

### dev

```shell
docker compose build
docker compose up
```

http://localhost:8000/ でアクセス可能

NOTE: `django.db.utils.OperationalError: connection to server at "db" (172.27.0.2), port 5432 failed: FATAL:  database "hello_django_dev" does not exist`
が出た場合は、ボリュームを削除してから`docker-compose exec web python manage.py migrate --noinput`を実行する


### prod

```shell
docker compose -f compose.prod.yaml up -d --build
docker compose -f compose.prod.yaml exec web python manage.py migrate --noinput
docker compose -f compose.prod.yaml exec web python manage.py collectstatic --no-input --clear
```

NOTE: -dオプションをつけることでバックグラウンドで起動する
--buildオプションをつけることで強制的にビルドする
-f オプションをつけることでファイルを指定する
[-f を使い、Compose ファイルの名前とパスを指定](https://docs.docker.jp/compose/reference/index.html#f-compose)

http://localhost:1337/ でアクセス可能


## コンテナの停止とボリュームの削除

NOTE: -vオプションをつけることでボリュームも削除される
ボリュームを削除 = データが消える

```shell
docker compose down -v
```

### devとprodを切り替える時

NOTE: devとprodを切り替える場合、ボリュームを削除してから切り替える必要がありそう