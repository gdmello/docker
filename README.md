### Delete all (running/non-running) containers that match image name
```bash
docker rm -f $(docker ps -a | grep rabbitmq | awk '{print $1}')
```

### Delete all (running/non-running) containers
```bash
docker rm -f $(docker ps -aq')
```

### Delete all images
```bash
docker rmi -f $(docker images -aq)
```
