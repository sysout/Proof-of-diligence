
## start/resume a container
```bash
docker start ubuntu
docker start 7cbaf16157f6
```

## login in to a running container / reattach the terminal & stdin
```bash
docker attach 7cbaf16157f6
docker exec -it ubuntu /bin/bash
```

## detach from a container without stopping it
- <kbd>Ctrl+p, Ctrl+q</kbd>

## show running containers
```bash
docker ps
```

## show all containers
```bash
docker ps -a
```

## show changes in the root directory
```bash
docker diff ubuntu|grep /root
```
