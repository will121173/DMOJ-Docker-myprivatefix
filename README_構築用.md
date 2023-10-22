1. docker + compose環境を準備します
1. このリポジトリをクローンします
1. このreadmerと同じディレクトリで`docker compose up -d`します（-dはバックグラウンド実行オプション）
1. [http://パブリックipアドレス:8080](http://パブリックipアドレス:8080)にアクセスしてトップページへ
1. 終わらせるときは`docker compose down`

- 8080番ポートをwebアクセス用に開けてください
- メモリ量は待機状態で1.5GB、変動分はユーザー数*10MB~50MBくらいが目安？
- cpuはアプリの性質上割といくらでも使えてしまうけれどどの程度並列実行してくれるかわからないのであまり拘っても仕方ないかも
- mysql-dataがデータの永続化用フォルダです、コンテナは落としてもいいけれどホスト端末のこのフォルダは残してください

### インターネット接続なしで使うために
- どこかの環境でdocker compose up した後imageを保存しておく ※15GB近くになる

```
docker compose up
docker compose down
```

```
docker save redis -o image_redis.tar
docker save mysql -o image_mysql.tar
docker save goropikari/dmoj-judger -o image_judger.tar
docker save goropikari/dmoj-site -o image_site.tar
```

- 本番環境にファイルを移して読み込む
```
docker load -i image_redis.tar
docker load -i image_mysql.tar
docker load -i image_judger.tar
docker load -i image_site.tar
```
```
docker compose up
```
