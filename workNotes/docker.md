notes docker docker-compose

# Docker

## Manipulate docker containers
- list containers
```bash
sudo docker ps
```
- stop container
```bash
sudo docker stop <CONTAINER_NAME>
```

## Manipulate Volumes

Problem: changed `.env` file but even after removing docker container with `rm` and using `docker compose up` again the database name and user was the same.
<br>Solution: remove volume

- list volumes
```bash
sudo docker volume ls
```
- inspect volume
```bash
sudo docker volume inspect <VOLUME_NAME>
```
- remove volume (after deleting container)
```bash
sudo docker volume rm <VOLUME_NAME>
```

## [Docker Compose](https://medium.com/codex/docker-compose-explained-3954baf495ec)
- [medium article](https://medium.com/codex/docker-compose-explained-3954baf495ec)

### Usage
Create containers using the command docker-compose up.
Please use detach mode using -d.

```bash
#docker-compose -f file_name up -d
docker-compose -f mysql.yaml up -d
```

In case of [port binging error](https://stackoverflow.com/questions/47069540/docker-compose-postgres-5432-bind-address-already-in-use-error) like: 
<br>docker-compose up cannot start service postgres: driver failed programming external connectivity on endpoint
<br><br>A) stop local postgresql with:
```bash
sudo service postgresql stop
```

You can stop postgres to start every time one the machine starts with:
```bash
sudo update-rc.d postgresql disable
```
<br>B) Change post assignment in `docker-compose.yml` file:
    ```bash
    ports:
      - '5433:5432'
    ```

    And run `docker-compose` up again.


The created docker container can be listed with:
```bash
docker ps
```

### Connect to docker container
```bash
docker exec -it <container_id> bash
```
- `-it` will make the connection interactive




Stop the created container using the command docker-compose down.
```bash
docker-compose -f mysql.yaml down
```




## Old notes:
to start docker
sudo docker-compose up in terminal

to see containers running
sudo docker ps

to connect to postgres
sudo docker exec -it <container-name> psql postgres

-it makes it interaktiv
