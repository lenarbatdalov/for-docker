# README

### clearing
```
docker rm $(docker ps -qa)
docker rmi $(docker images -qa)

docker ps -a
docker images -a

Если осталось, то можно по хардкору
docker image rm $(docker image ls -a -q) -f
```

