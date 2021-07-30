
## 给应网站添加一个应用路径

通常一个网站都是部署在根目录的，但是由于特殊情况，某些网站需要部署到指定的路径下。

前提：网站必须要保证所有的连接输出中都必须要包含应用程序路径。
Demo设置应用程序路径为application_path

Environment

```shell
export VERSION=test
export DOCKER_CONTEXT_PATH=nginx_study
export IMAGENAME=application_path

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
docker run --name ${IMAGENAME} --rm --detach --publish 8080:80  ${DOCKER_REGISTRY:+${DOCKER_REGISTRY}/}${DOCKER_CONTEXT_PATH:+${DOCKER_CONTEXT_PATH}/}${IMAGENAME}:${VERSION}
```

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

