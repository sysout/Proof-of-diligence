
# start container
```
docker start ubuntu
```

# login in to a running container
```
docker exec -it ubuntu /bin/bash
```

# show running containers
```
docker ps
```

# show all containers
```
docker ps -a
```

# show changes in the root directory
```
docker diff ubuntu|grep /root
```
