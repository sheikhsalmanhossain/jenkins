## Docker:

### Running Jenkins image as docker container:

```
docker run -p 8080:8080 Jenkins/Jenkins:latest
```

### Execute CMD inside docker container :
```
docker exec -it container_id bash
```

### Running Jenkins in a docker container using docker compose :

```
version: '3'
services:
  Jenkins:
    image: Jenkins/Jenkins:latest
    ports:
      - "8080:8080"

```
