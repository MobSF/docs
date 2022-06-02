# Opciones de MobSF con Docker

!> El Análisis Dinámico no está soportado cuando se usa Docker

?> ¿Es demasiado trabajo la configuración de MobSF? Usa la imagen precompilada más nueva desde [DockerHub](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/).

**Imagen precompilada de DockerHub**

```bash
docker pull opensecurity/mobile-security-framework-mobsf
# Solo Análisis Estático
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

**Para una imagen persistente**

```bash
mkdir <your_local_dir>
chown 9901:9901 <your_local_dir>
docker run -it --rm --name mobsf -p 8000:8000 -v <your_local_dir>:/home/mobsf/.MobSF opensecurity/mobile-security-framework-mobsf:latest
```

**Construir una imagen desde un Dockerfile**

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
docker build -t mobsf .
docker run -it --rm -p 8000:8000 mobsf
```

**Construir una imagen desde un Dockerfile detrás de un proxy**

```bash
docker build --build-arg https_proxy="https://${PROXY_IP}:${PROXY_PORT}" --build-arg http_proxy="${PROXY_IP}:${PROXY_PORT}" --build-arg NO_PROXY="127.0.0.1" -t mobsf .
```

Configura la variable de ambiente `PROXY_IP` con el valor de la dirección IP de tu proxy y `PROXY_PORT` con el puerto que usa el este.

**Reconstruir la imagen de un Dockerfile desde cero**

```bash
docker rmi ubuntu:18.04
docker build --no-cache --rm -t mobsf .
```

**Para soporte de PostgreSQL**

Necesitarás docker-compose (véase <https://docs.docker.com/compose/install>).

* Construir las imagenes

`docker-compose build`

* Iniciar los servicios

`docker-compose up ` (en primer plano )

o

`docker-compose up -d`  (en segundo plano)

Después verifica que los dos servicios se encuentran activos:

`docker ps`

```bash
CONTAINER ID        IMAGE                                   COMMAND                  CREATED             STATUS              PORTS                          NAMES
7de107c5b853        mobile-security-framework-mobsf_mobsf   "python3 manage.py r…"   5 weeks ago         Up 5 weeks          0.0.0.0:8000->8000/tcp         mobile-security-framework-mobsf_mobsf_1
149a3ffa61ca        postgres:latest                         "docker-entrypoint.s…"   5 weeks ago         Up 5 weeks          5432/tcp                       mobile-security-framework-mobsf_postgres_1
```

**Para ver lo que pasó en el contenedor si se inicia con `-d` en vez de `-it`**

```bash
docker logs -f --tail 100 mobsf
```

**Para tener acceso a la shell del contenedor**

```bash
docker exec -it mobsf /bin/bash
```
