# MobSF Dockerオプション

!> 動的解析はDockerではサポートされていません。

?> MobSFの設定が面倒だなと思いますか？[DockerHub](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/) にある最新のビルド済イメージを使ってください。

**DockerHubのビルド済Dockerイメージ**

```bash
docker pull opensecurity/mobile-security-framework-mobsf
# 静的解析のみ
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

**ARM64/Apple M1ユーザー向けDockerイメージ**

```bash
docker pull opensecurity/mobile-security-framework-mobsf:arm
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:arm
```

**永続化の設定**

```bash
docker run -it --rm --name mobsf -p 8000:8000 -v <your_local_dir>:/home/mobsf/.MobSF opensecurity/mobile-security-framework-mobsf:latest
```

**Dockerfileからのイメージのビルド**

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
docker build -t mobsf .
docker run -it --rm -p 8000:8000 mobsf
```

**Proxy内部でのDockerfileからのイメージのビルド**

```bash
docker build --build-arg https_proxy="https://${PROXY_IP}:${PROXY_PORT}" --build-arg http_proxy="${PROXY_IP}:${PROXY_PORT}" --build-arg NO_PROXY="127.0.0.1" -t mobsf .
```

環境変数`PROXY_IP`にはプロキシIPアドレスの値を設定し、`PROXY_PORT`には使用するプロキシポートを設定します。

**Dockerfileからイメージを再構築する**

```bash
docker rmi ubuntu:18.04
docker build --no-cache --rm -t mobsf .
```

**postgresサポート**

docker-composeを利用する必要があります。 (参照: <https://docs.docker.com/compose/install>).

* イメージのビルド

`docker-compose build`

* サービスの起動

`docker-compose up -d`  (バックグラウンドで実行)

または

`docker-compose up ` (フォアグラウンドで実行)

すると二つのサービスが起動していることを確認できます:

`docker ps`

```bash
CONTAINER ID        IMAGE                                   COMMAND                  CREATED             STATUS              PORTS                          NAMES
7de107c5b853        mobile-security-framework-mobsf_mobsf   "python3 manage.py r…"   5 weeks ago         Up 5 weeks          0.0.0.0:8000->8000/tcp         mobile-security-framework-mobsf_mobsf_1
149a3ffa61ca        postgres:latest                         "docker-entrypoint.s…"   5 weeks ago         Up 5 weeks          5432/tcp                       mobile-security-framework-mobsf_postgres_1
```

**`-it`の代わりに`-d`を指定して実行した場合、コンテナ内で何が起きているかを確認**

```bash
docker logs -f --tail 100 mobsf
```

**コンテナ内でにシェルでアクセス**

```bash
docker exec -it mobsf /bin/bash
```
