## isucon7-qualify

- Clone from https://github.com/isucon/isucon7-qualify
  - README に予選マニュアルが載ってるのでよく読むこと
- Build with https://github.com/matsuu/docker-isucon/tree/master/isucon7-qualifier
  - Docker 周りの設定はここから拝借した
  - See. http://isucon.net/archives/54946542.html#docker

### 起動

ベンチマーク以外の Docker を構築&起動する。そこそこ時間がかかる。

```
docker-compose up -d db
docker-compose up -d app
docker-compose up -d web
```

db は起動時に流し込みがあるため時間がかかる。ログに「MySQL init process done. Ready for start up.」の文字列があれば ok。

```
docker-compose logs db | grep 'done'
```

動作確認

```
open http://127.0.0.1
```

### ベンチマーク

```
docker-compose up bench
```

### ログイン

```
docker-compose exec web bash
docker-compose exec app bash
docker-compose exec db bash
```

### チューニングの仕方

- `docker/app/xxx/` の Dockerfile を `webapp/xxx/` に置き、Dockerfile と docker-compose.yml を書き換える（[参考 Commit](https://github.com/daido1976/isucon7-qualify/commit/e7632dd6a2d6e129ed698d95cec9bd06cdd32ac7)）
- 上記を行ってから `$ docker-compose up -d --build app`
