# django-on-docker

testdriven.ioの[Dockerizing Django with Postgres, Gunicorn, and Nginx](https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/)を写経したリポジトリ

## 起動方法

### prod

```shell
docker compose -f docker-compose.prod.yml up -d --build
docker compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
docker compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
```

NOTE: -dオプションをつけることでバックグラウンドで起動する
--buildオプションをつけることで強制的にビルドする

http://localhost:1337/ でアクセス可能


## コンテナの停止とボリュームの削除

NOTE: -vオプションをつけることでボリュームも削除される
ボリュームを削除 = データが消える

```shell
docker compose down -v
```