notes  -compose

# Docker 

## Manipulate docker containers
- list containers

Running conianers only:
```bash
sudo docker ps
```
All containers:
```bash
sudo docker ps -a
```
- stop container
```bash
sudo docker stop <CONTAINER_NAME>
```

## Manipulate Volumes

Problem: changed `.env` file but even after removing docker container with `rm` and using `docker compose up` again the database name and user was the same.
<br>Solution: remove volume

- list docker volumes
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
Create container:

```bash
#-compose -f file_name up -d
docker compose up -d <docker-compose-file-name.yaml> 
```
`-d` runs it in the background

In case of [port binging error](https://stackoverflow.com/questions/47069540/-compose-postgres-5432-bind-address-already-in-use-error) like: 
<br>-compose up cannot start service postgres: driver failed programming external connectivity on endpoint
<br><br>A) stop local postgresql with:
```bash
sudo service postgresql stop
```

You can stop postgres to start every time one the machine starts with:
```bash
sudo update-rc.d postgresql disable
```
<br>B) Change post assignment in `-compose.yml` file:
    ```bash
    ports:
      - '5433:5432'
    ```

    And run `-compose` up again.


The created  container can be listed with:
```bash
 ps
```

### Connect to  container
```bash
 exec -it <container_id> bash
```
- `-it` will make the connection interactive




Stop the created container using the command -compose down.
```bash
-compose -f mysql.yaml down
```




## Old notes:
to start 
sudo -compose up in terminal

to see containers running
sudo  ps

to connect to postgres
sudo  exec -it <container-name> psql postgres

-it makes it interaktiv
