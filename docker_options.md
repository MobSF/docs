# Docker Options

#### Prebuilt Docker image from DockerHub

```bash
docker pull opensecurity/mobile-security-framework-mobsf
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

#### For persistence

```bash
mkdir <your_local_dir>
chown -R 9901:9901 <your_local_dir>
docker run -it --rm --name mobsf -p 8000:8000 -v <your_local_dir>:/home/mobsf/.MobSF opensecurity/mobile-security-framework-mobsf:latest
```

#### Building Image from Dockerfile

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
docker build -t mobsf .
docker run -it --rm -p 8000:8000 mobsf
```

#### Building Image behind a proxy from Dockerfile

```bash
docker build --build-arg https_proxy="https://${PROXY_IP}:${PROXY_PORT}" --build-arg http_proxy="${PROXY_IP}:${PROXY_PORT}" --build-arg NO_PROXY="127.0.0.1" -t mobsf .
```

Set the environment variable `PROXY_IP` with the value of your proxy ip address and `PROXY_PORT` with the proxy port used.

#### Rebuilding Image from Dockerfile from Scratch

```bash
docker build --no-cache --rm -t mobsf .
```

#### To see the mobsf container logs

```bash
docker logs -f --tail 100 mobsf
```

#### For Postgres and Nginx reverse proxy support

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

### Architecture

```mermaid
graph TD
    subgraph DockerNetwork ["Docker Network: mobsf_network"]
        direction LR
        postgres[(Postgres DB)]
        nginx[/Nginx\]
        mobsf{{MobSF}}
    end

    host[/Host Machine\]

    host --> |"Volume:<br/>$HOME/MobSF/<br/>postgresql_data"| postgres
    host --> |"Volume:<br/>./nginx.conf"| nginx
    host --> |"Volume:<br/>$HOME/MobSF/<br/>mobsf_data"| mobsf
    
    nginx -.- |"Depends on"| mobsf
    mobsf -.- |"Depends on"| postgres

    nginx === |"Port: 80:4000<br/>Port: 1337:4001"| host

    mobsf -.- |"Extra host:<br/>host.docker.internal"| host

    %% Add invisible nodes for spacing
    inv1((( )))
    inv2((( )))
    inv3((( )))
    inv4((( )))

    %% Position invisible nodes
    host --- inv1
    inv2 --- DockerNetwork
    DockerNetwork --- inv3
    inv4 --- host

    classDef container fill:#e0f7fa,stroke:#006064,stroke-width:2px;
    class postgres,nginx,mobsf container;
    
    classDef network fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px,rx:5,ry:5;
    class DockerNetwork network;

    classDef host fill:#fff3e0,stroke:#e65100,stroke-width:2px;
    class host host;

    classDef invisible fill:none,stroke:none;
    class inv1,inv2,inv3,inv4 invisible;

    linkStyle 0,1,2 stroke:#1565c0,stroke-width:2px;
    linkStyle 3,4 stroke:#7b1fa2,stroke-width:2px,stroke-dasharray: 5 5;
    linkStyle 5 stroke:#c62828,stroke-width:3px;
    linkStyle 6 stroke:#2e7d32,stroke-width:2px,stroke-dasharray: 5 5;
```

**Docker Compose Configuration for MobSF**

This configuration sets up a multi-container environment for running MobSF with PostgreSQL and Nginx.

Services:

1. postgres
   - Image: PostgreSQL 13
   - Purpose: Provides the database backend for MobSF
   - Configuration:
     * Persistent volume for data storage
     * Environment variables for database credentials
     * Connected to mobsf_network

2. nginx
   - Image: Latest Nginx
   - Purpose: Acts as a reverse proxy and web server
   - Configuration:
     * Exposes ports 80 and 1337
     * Custom Nginx configuration file mounted
     * Depends on mobsf service
     * Connected to mobsf_network

3. mobsf
   - Image: Latest MobSF
   - Purpose: Runs the Mobile Security Framework application
   - Configuration:
     * Volume mounted for data persistence
     * Environment variables for PostgreSQL connection
     * Depends on postgres service
     * Extra host configuration for Docker host access required for adb connectivity
     * Connected to mobsf_network

Network:
   - A custom bridge network 'mobsf_network' is created for inter-service communication

Note: All services are configured to restart automatically in case of failures.
