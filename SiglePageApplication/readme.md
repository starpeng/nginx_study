
## 单页应用程序

现代的前端框架多数采用单页应用程序模式，入口点只有默认的 index.html，当前端的路由方案使用 history 模式时，如果用户刷新浏览器，那么服务器后端其实上并没有对应地址的文件。
如果服务端没有正确处理，前端将会得到 404 的异常返回，需要通过 NGINX 重定向输出首页的 index.html 即可。

Environment

```shell
export VERSION=test
export DOCKER_CONTEXT_PATH=nginx_study
export IMAGENAME=spa

```

Build

```shell
docker build --rm \
    --build-arg IMAGENAME=${IMAGENAME} \
    --build-arg DOCKER_REGISTRY=${DOCKER_REGISTRY} \
    --build-arg DOCKER_CONTEXT_PATH=${DOCKER_CONTEXT_PATH} \
    --build-arg VERSION=${VERSION} \
    --build-arg BUILD_DATE=$(date +%FT%T%Z) \
    -t ${DOCKER_REGISTRY:+${DOCKER_REGISTRY}/}${DOCKER_CONTEXT_PATH:+${DOCKER_CONTEXT_PATH}/}${IMAGENAME}:${VERSION} .; 
```

Run
```shell
docker run --name ${IMAGENAME} --rm --detach --publish 8080:8080  ${DOCKER_REGISTRY:+${DOCKER_REGISTRY}/}${DOCKER_CONTEXT_PATH:+${DOCKER_CONTEXT_PATH}/}${IMAGENAME}:${VERSION}
```

访问：http://127.0.0.1:8080

Clean

```shell
# Stopping nginx_study containers...
docker ps -qf "label=project=nginx_study" | xargs -r docker stop

# Removing nginx_study images...
docker images -qf "label=project=nginx_study" | xargs -r docker rmi

# Cleaning dangling images...
docker images -qf "dangling=true" | xargs -r docker rmi

# Pruneing images...
docker image prune -f
```

