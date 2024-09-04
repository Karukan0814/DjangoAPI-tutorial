# 開発環境の構築

https://qiita.com/bakupen/items/f23ce3d2325b4491a2dd
を参考にした。
ただし、以下を変更した。
・mysqlを5.7→8.0にアップグレード
・requirements.txtに　djangorestframework==3.15.2　を追記

開発環境を Docker を使用して立ち上げることが可能。以下、その手順。

1. 当該レポジトリをローカル環境にコピー

2. settings.pyの変更
   　settings.pyのDATABASESを以下のように記述して保存する。
   ※環境変数ファイルについてはあとで考える

```
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.mysql",
        "NAME": "django-db",
        "USER": "django",
        "PASSWORD": "django",
        "HOST": "db",
        "PORT": "3306",
    }
}

```

3. Docker ビルド
   　以下を実行してビルド。なお、以下は Docker がインストール済みであることを前提とする。

```
docker compose build
```

4. Docker 立ち上げ
   　以下を実行してコンテナを立ち上げ。

```
docker compose up -d
```

5. DB Migration 実行
   　以下を実行して初期テーブルの構築。

```
docker-compose exec web python manage.py migrate

```

6. 動作確認
   　[http://127.0.0.1:8000/](http://127.0.0.1:8000/)にアクセスして動作確認
