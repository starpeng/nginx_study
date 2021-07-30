FROM nginx:stable
COPY /app/ /usr/share/nginx/html/application_path/
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Metadata params
ARG VERSION=0.0.1
ARG DOCKER_REGISTRY
ARG DOCKER_CONTEXT_PATH=nginx_study
ARG BUILD_DATE
ARG IMAGENAME

# Metadata
LABEL org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.name=$IMAGENAME \
    org.label-schema.description="Nginx Study, web with application path" \
    org.label-schema.url="https://github.com/starpeng/nginx_study" \
    org.label-schema.vcs-url="https://github.com/starpeng/nginx_study" \
    org.label-schema.vendor=starpeng \
    org.label-schema.version=$VERSION \
    org.label-schema.docker.schema-version="1.0" \
    org.label-schema.docker.cmd=docker="run -it -p 8080:80  ${DOCKER_REGISTRY:+${DOCKER_REGISTRY}/}${DOCKER_CONTEXT_PATH:+${DOCKER_CONTEXT_PATH}/}${IMAGENAME}:${VERSION}" \
    project=nginx_study
