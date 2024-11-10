# MobSF Docker Options

**Prebuilt Docker image from DockerHub**

```bash
docker pull opensecurity/mobile-security-framework-mobsf
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

**For persistence**

```bash
mkdir <your_local_dir>
chown -R 9901:9901 <your_local_dir>
docker run -it --rm --name mobsf -p 8000:8000 -v <your_local_dir>:/home/mobsf/.MobSF opensecurity/mobile-security-framework-mobsf:latest
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
docker build --no-cache --rm -t mobsf .
```

**To see the mobsf container logs**

```bash
docker logs -f --tail 100 mobsf
```

**For postgres support**

```bash
# Install docker compose.
cd docker

# Download the latest images 
docker compose pull

# Launch the services
docker compose up

# or run in the background
docker compose up -d

# See logs from mobsf container
docker compose logs -f mobsf 

# Stop the containers
docker compose down
```
