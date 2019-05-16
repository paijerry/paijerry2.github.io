# Dockerfile

---

[RUN vs CMD vs ENTRYPOINT - 每天5分钟玩转 Docker 容器技术（17） - 每天5分钟玩转 OpenStack Blog](https://www.ibm.com/developerworks/community/blogs/132cfa78-44b0-4376-85d0-d3096cd30d3f/entry/RUN_vs_CMD_vs_ENTRYPOINT_%E6%AF%8F%E5%A4%A95%E5%88%86%E9%92%9F%E7%8E%A9%E8%BD%AC_Docker_%E5%AE%B9%E5%99%A8%E6%8A%80%E6%9C%AF_17?lang=en)

##  docker build note

1. go build
```sh
GOOS=linux GOARCH=amd64 go build -o ezrefund
```

2. write Dockerfile
```Dockerfile
FROM alpine:3.5
MAINTAINER jerry

ADD ezrefund /

EXPOSE 13227

CMD /ezrefund server -p 13227
```

3. docker build image
```sh
docker build -t ezrefund .
```

4. check docker image is build or not
```sh
docker image ls | grep ezrefund
```

5. docker run

test mode: get into cli interface and will be removed after shut down the process
```sh
docker run -it --rm -p 13227:13227  ezrefund
# or (dockerfile no CMD)
docker run -it --rm -p 13227:13227  ezrefund /ezrefund server -p 13227
```

Detached mode: Run container in the background, print new container id
```sh
docker run -d -p 13227:13227  ezrefund
# or (dockerfile no CMD)
docker run -d -p 13227:13227  ezrefund /ezrefund server -p 13227
```

6. check docker container is running or not
```sh
docker ps
```
---
