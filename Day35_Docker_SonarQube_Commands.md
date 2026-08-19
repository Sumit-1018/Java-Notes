# Day 35 - Docker & SonarQube Commands Reference
*Fri, 14 Aug 2026*

Builds on the Docker concepts from Day 30 (Container/Image basics) and the static-analysis concepts from Day 4 (SonarLint/SonarQube) — this is the hands-on command reference for both.

## Docker Commands

### Checking Docker Itself

```bash
docker --version                   # check installed Docker version
docker info                        # detailed system-wide Docker info
```

### Images

```bash
docker images                      # list all local images
docker pull <image>:<tag>          # download an image from a registry (e.g. Docker Hub)
docker build -t <name>:<tag> .     # build an image from a Dockerfile in current dir
docker rmi <image-id>              # remove an image
docker tag <image> <new-name>      # tag an image with a new name/version
docker push <name>:<tag>           # push an image to a registry
docker history <image>             # show the layers that make up an image
```

### Containers — Running & Managing

```bash
docker run <image>                             # run a container from an image
docker run -d <image>                          # run in detached mode (background)
docker run -p 8080:8080 <image>                # map host port 8080 to container port 8080
docker run --name myapp <image>                # give the container a name
docker run -e VAR=value <image>                # pass an environment variable
docker run -v /host/path:/container/path <image>  # mount a volume
docker run -it <image> /bin/bash               # run interactively with a shell attached
```

```bash
docker ps                          # list running containers
docker ps -a                       # list ALL containers, including stopped
docker stop <container-id>         # gracefully stop a running container
docker start <container-id>        # start a stopped container
docker restart <container-id>      # restart a container
docker rm <container-id>           # remove a stopped container
docker rm -f <container-id>        # force-remove a running container
```

### Inspecting & Debugging

```bash
docker logs <container-id>         # view container logs
docker logs -f <container-id>      # follow logs in real time
docker exec -it <container-id> /bin/bash   # open a shell inside a running container
docker inspect <container-id>      # full JSON details of a container
docker stats                       # live CPU/memory usage of running containers
docker top <container-id>          # processes running inside a container
```

### Cleanup

```bash
docker system prune                # remove unused containers, networks, dangling images
docker system prune -a             # also remove all unused images (not just dangling)
docker container prune             # remove all stopped containers
docker image prune                 # remove dangling images
docker volume prune                # remove unused volumes
```

### Dockerfile — Building a Spring Boot Image

```dockerfile
FROM eclipse-temurin:21-jre
WORKDIR /app
COPY target/myapp.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

```bash
docker build -t myapp:1.0 .
docker run -d -p 8080:8080 --name myapp-container myapp:1.0
```

### Docker Compose — Multi-Container Apps

`docker-compose.yml` defines multiple services that run together.

```yaml
version: "3.8"
services:
  app:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - db
  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
    ports:
      - "3306:3306"
```

```bash
docker compose up                  # start all services
docker compose up -d               # start in detached mode
docker compose down                # stop and remove all services
docker compose logs -f             # follow logs across all services
docker compose ps                  # list running services
docker compose build               # rebuild service images
```

### Volumes & Networks

```bash
docker volume create myvolume      # create a named volume
docker volume ls                   # list volumes
docker volume inspect myvolume     # inspect a volume

docker network create mynetwork    # create a custom network
docker network ls                  # list networks
docker network connect mynetwork <container>   # attach a container to a network
```

---
## SonarQube Commands

Builds on the SonarLint/SonarQube concepts from Day 4 — SonarLint flags issues live in the IDE, while SonarQube runs full project-wide scans, typically as a CI/CD step.

### Running SonarQube Server Locally (Docker)

```bash
docker run -d --name sonarqube -p 9000:9000 sonarqube:lts-community
```
Then open `http://localhost:9000` (default login: `admin` / `admin`).

### SonarScanner — Analyzing a Project

**Standalone scanner (any project type):**
```bash
sonar-scanner \
  -Dsonar.projectKey=my-project \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<your-token>
```

**Maven-based project:**
```bash
mvn sonar:sonar \
  -Dsonar.projectKey=my-project \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<your-token>
```

**Gradle-based project:**
```bash
./gradlew sonar \
  -Dsonar.projectKey=my-project \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<your-token>
```

### `sonar-project.properties` — Standalone Config File

Sits at the project root instead of passing every flag on the command line.

```properties
sonar.projectKey=my-project
sonar.projectName=My Project
sonar.sources=src/main/java
sonar.tests=src/test/java
sonar.java.binaries=target/classes
sonar.sourceEncoding=UTF-8
sonar.host.url=http://localhost:9000
```

### Combining With Test Coverage (JaCoCo — see Day 23)

```bash
mvn clean verify sonar:sonar \
  -Dsonar.projectKey=my-project \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<your-token> \
  -Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml
```

### Quality Gate — Checking Pass/Fail in CI

```bash
# After a scan, poll the Quality Gate status via the Web API
curl -u <your-token>: \
  "http://localhost:9000/api/qualitygates/project_status?projectKey=my-project"
```
A CI pipeline typically fails the build if this returns `"status": "ERROR"` (see the Quality Gate concept from Day 4).

### Useful Web API Endpoints

| Endpoint | Purpose |
|---|---|
| `/api/issues/search?projectKeys=my-project` | List all issues (bugs, smells, vulnerabilities) for a project |
| `/api/measures/component?component=my-project&metricKeys=coverage,bugs,vulnerabilities` | Fetch specific metrics |
| `/api/qualitygates/project_status` | Check current Quality Gate pass/fail status |
| `/api/projects/search` | List all projects on the server |

### Typical GitLab CI Integration (ties back to Day 34)

```yaml
sonarqube-check:
  stage: test
  script:
    - mvn verify sonar:sonar
        -Dsonar.projectKey=my-project
        -Dsonar.host.url=$SONAR_HOST_URL
        -Dsonar.login=$SONAR_TOKEN
  only:
    - main
    - merge_requests
```
`$SONAR_HOST_URL` and `$SONAR_TOKEN` are typically stored as **masked CI/CD variables** in GitLab (Settings → CI/CD → Variables) rather than hardcoded.
