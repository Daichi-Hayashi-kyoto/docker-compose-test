# Docker-composeを用いた機械学習の簡単なシステム構築のテスト

## docker-composeの起動

以下のディレクトリ構造になっており，以下ではdb-server_and_analysisのディレクトリ下にいるとする．

```
db-server_and_analysis/
├── Dockerfile-db
├── Dockerfile-jupyter
├── README.md
├── docker-compose.yml
└── scripts
    └── initdb
        └── init_table.sql
```

- 以下のコマンドにより，dockerファイルを起動する

```
docker-compose build
docker-compose up -d
```

- そして，以下のコマンドでサーバーが立ち上がっていることを確認する．

```
docker-compose ps

> > >

      Name                  Command               State           Ports         
------------------------------------------------------------------------------
ml_db_1        docker-entrypoint.sh postgres    Up      0.0.0.0:5432->5432/tcp
ml_jupyter_1   tini -g -- /bin/sh -c jupy ...   Up      0.0.0.0:8888->8888/tcp
```

- その後，`docker exec ml_jupyter_1 jupyter notebook list`コマンドを打てば以下が出力される． ```

Currently running servers: <http://0.0.0.0:8888/?token=> xxxxxxx :: /opt/analysis

```

- そこで，`http://0.0.0.0:8888/?token= xxxxxxx`の部分をコピーしてjupyterが起動しているか確認する． -

- 次のコマンドでコンテナを停止する
```

docker-compose stop

> > > Stopping ml_jupyter_1 ... done Stopping ml_db_1 ... done ```

## Docker-compose.yml

- Docker Compose起動時に起点となるファイル
- その他のファイルはこのファイルに記載されている内容を元に参照する

## .envファイル

- 環境変数の設定を行なっているファイル
