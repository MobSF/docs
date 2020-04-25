# MobSF Docker 选项

!> 动态分析不支持Docker方式

?> 不愿去设置MobSF？使用最新的预构建镜像 [DockerHub](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/).

**使用Docker镜像**

```bash
docker pull opensecurity/mobile-security-framework-mobsf
# 只能运行静态扫描
docker run -it -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

**持久化**

```bash
docker run -it --name mobsf -p 8000:8000 -v <your_local_dir>:/root/.MobSF opensecurity/mobile-security-framework-mobsf:latest
```

**从Dockerfile构建镜像**

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
docker build -t mobsf .
docker run -it -p 8000:8000 mobsf
```

**在Dockerfile的代理后边构建镜像**

```bash
docker build --build-arg https_proxy="https://${PROXY_IP}:${PROXY_PORT}" --build-arg http_proxy="${PROXY_IP}:${PROXY_PORT}" --build-arg NO_PROXY="127.0.0.1" -t mobsf .
```

使用代理IP地址的值设置环境变量"PROXY_IP"，并使用所使用的代理端口设置"PROXY_PORT"。

**从头开始构建镜像**

```bash
docker rmi ubuntu:18.04
docker build --no-cache --rm -t mobsf .
```

**Posgres的支持**

你需要 docker-compose , (链接: <https://docs.docker.com/compose/install>).

* 构建镜像

`docker-compose build`

* 启动服务

`docker-compose up -d`  (后台运行)

or

`docker-compose up ` (在前台执行)

然后验证2个服务是否启动：:

`docker ps`

```bash
CONTAINER ID        IMAGE                                   COMMAND                  CREATED             STATUS              PORTS                          NAMES
7de107c5b853        mobile-security-framework-mobsf_mobsf   "python3 manage.py r…"   5 weeks ago         Up 5 weeks          0.0.0.0:8000->8000/tcp         mobile-security-framework-mobsf_mobsf_1
149a3ffa61ca        postgres:latest                         "docker-entrypoint.s…"   5 weeks ago         Up 5 weeks          5432/tcp                       mobile-security-framework-mobsf_postgres_1
```

如果您不想使用docker-compose，则需要先启动一个postgres容器，然后使用`build-arg`来启动MobSF容器。
**POSTGRES=True**.

```bash
docker build --build-arg POSTGRES=True -t mobsf .
```

您可以在`postgres_support.sh`中更改postgres连接信息。

**必须在构建映像之前完成此操作**

```bash
#!/bin/bash
set -e
POSTGRES=$1
echo "Postgres support : ${POSTGRES}"
if [ "$POSTGRES" == True ]; then
 echo "Installing Postgres"
 pip3 install psycopg2-binary
 #Enable postgres support
 sed -i '/# Sqlite3 suport/,/# End Sqlite3 support/d' ./MobSF/settings.py && \
 sed -i "/# Postgres DB - Install psycopg2/,/'''/d" ./MobSF/settings.py && \
 sed -i "/# End Postgres support/,/'''/d" ./MobSF/settings.py && \
 sed -i "s/'PASSWORD': '',/'PASSWORD': 'password',/" ./MobSF/settings.py && \
 sed -i "s/'HOST': 'localhost',/'HOST': 'postgres',/" ./MobSF/settings.py
fi
````

**如果您在第一次启动时遇到错误**

```bash
docker exec -it mobile-security-framework-mobsf_mobsf_1 python3 manage.py makemigrations
docker exec -it mobile-security-framework-mobsf_mobsf_1 python3 manage.py makemigrations StaticAnalyzer
docker exec -it mobile-security-framework-mobsf_mobsf_1 python3 manage.py migrate
```

**看看如果使用`-d`而不是`-it`, 容器中发生了什么**

```bash
docker logs -f --tail 100 mobsf
```

**在容器中执行shell**

```bash
docker exec -it mobsf /bin/bash
```
