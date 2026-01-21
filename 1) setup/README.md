## Docker:

## 1) :

### Running Jenkins image as docker container:

```
docker run -p 8080:8080 Jenkins/Jenkins:latest
```

### Execute CMD inside docker container :

```
docker exec -it container_id bash
```

## 2) :

### Running Jenkins in a docker container using docker compose :

```
version: '3'
services:
  Jenkins:
    image: Jenkins/Jenkins:latest
    ports:
      - "8080:8080"

```

## 3) : Run Jenkins with docker run :

Create a Docker volume for Jenkins data:

``` docker volume create jenkins_home ```

Run Jenkins container:

```
docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts
```

Get the initial admin password:

``` docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword ```

Open Jenkins in browser:

``` http://localhost:8080 ```

## 4) : Jenkins using Docker Compose :

Create docker-compose.yml

```
version: "3.8"

services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    restart: unless-stopped
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock

volumes:
  jenkins_home:
```

Start Jenkins:
``` docker compose up -d ```

Get admin password :
``` docker compose exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword ```
