# amazonlinux2 base python django development dockerimages

## 概要

amazonlinux2 をベースにした django 開発環境
以下の外部システムを利用してできるだけ実行環境下に近い形を想定

- minio
- redis
- mysql5.7

## セットアップ方法

docker network を利用しているため docker command を利用して network を作成しておく

```
$> docker network create development
```

```
$> git clone https://xxx.git
$> cd xxx
$> docker-compose up -d --build

実行ユーザを指定してdjango実行サーバに接続する
$> docker-compose exec django runuser -l appuser
```

## 登録用　 user & group

appcreators
appadmin

appuser
admin

## mount volumes

windows toolbox

```
 /c/Users/$USERNAME/<pathto>
```

linux

```
 $HOME/<pathto>
```

## container の概要

### コンテナ共通の設定

confd entrykit の組み合わせで常駐化しており cron が動作している前提としている
container からは systemd が利用できないため confd のリロードを実行し、cron を実行させて動作を終えるようにしている

mysql

redis

minii

## django container

主に開発サーバとなるコンテナ　 docker attach などで入り込んで直接操作を行う

```
 $> docker-compose build django
 $> docker-compose up -d django
 $> docker-compose exec django bash
```

/work フォルダを django project の配置場所としている

django-project の配置

```
 $> cd /work
 $> git clone https://github.com/xxx.git
 $> cd <git clone dir>
 $> pip install -r requirements.txt
```

django container では pyenv をインストールしている python3.7.2
必要に応じて python を pyenv 経由でインストールする

## anyenv.exports

anyenv を導入しているので利用する env を導入
$> anyenv install -l
$> anyenv install <\*\*>env
