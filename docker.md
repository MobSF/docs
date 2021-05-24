# MobSF Docker Options

!> Dynamic Analysis is not supported with Docker

?> Feeling too lazy to setup MobSF? Use the latest prebuilt image from [DockerHub](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/).

**Prebuilt Docker image from DockerHub**

```bash
docker pull opensecurity/mobile-security-framework-mobsf
# Static Analysis Only
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

**Docker Image for ARM64/Apple M1 users***

```bash
docker pull opensecurity/mobile-security-framework-mobsf:arm
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:arm
```

**For persistence**

```bash
docker run -it --rm --name mobsf -p 8000:8000 -v <your_local_dir>:/root/.MobSF opensecurity/mobile-security-framework-mobsf:latest
```

**Building Image from Dockerfile**

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
docker build -t mobsf .
docker run -it --rm -p 8000:8000 mobsf
```

**Building Image behind a proxy from Dockerfile**

```bash
docker build --build-arg https_proxy="https://${PROXY_IP}:${PROXY_PORT}" --build-arg http_proxy="${PROXY_IP}:${PROXY_PORT}" --build-arg NO_PROXY="127.0.0.1" -t mobsf .
```

Set the environment variable `PROXY_IP` with the value of your proxy ip address and `PROXY_PORT` with the proxy port used.

**Rebuilding Image from Dockerfile from Scratch**

```bash
docker rmi ubuntu:18.04
docker build --no-cache --rm -t mobsf .
```

**For postgres support**

You will need docker-compose, (See: <https://docs.docker.com/compose/install>).

* Build the images 

`docker-compose build`

* Launch the services

`docker-compose up -d`  (in background)

or

`docker-compose up ` (in foreground )

Then verify the 2 services are up:

`docker ps`

```bash
CONTAINER ID        IMAGE                                   COMMAND                  CREATED             STATUS              PORTS                          NAMES
7de107c5b853        mobile-security-framework-mobsf_mobsf   "python3 manage.py r…"   5 weeks ago         Up 5 weeks          0.0.0.0:8000->8000/tcp         mobile-security-framework-mobsf_mobsf_1
149a3ffa61ca        postgres:latest                         "docker-entrypoint.s…"   5 weeks ago         Up 5 weeks          5432/tcp                       mobile-security-framework-mobsf_postgres_1
```

**To see what's happened in container if launched with `-d` instead of `-it`**

```bash
docker logs -f --tail 100 mobsf
```

**To have shell access in the container**

```bash
docker exec -it mobsf /bin/bash
```
