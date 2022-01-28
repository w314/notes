# Docker

## Docker Compose
https://medium.com/codex/docker-compose-explained-3954baf495ec

Create containers using the command docker-compose up.
Please use detach mode using -d.

```bash
#docker-compose -f file_name up -d
docker-compose -f mysql.yaml up -d
```

Stop the created container using the command docker-compose down.
```bash
docker-compose -f mysql.yaml down
```
