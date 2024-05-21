# django-on-docker

testdriven.ioの[Dockerizing Django with Postgres, Gunicorn, and Nginx](https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/)を写経したリポジトリ

## コンテナの停止とボリュームの削除

NOTE: -vオプションをつけることでボリュームも削除される
ボリュームを削除 = データが消える

```shell
docker compose down -v
```