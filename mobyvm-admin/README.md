DOCKER_BUILDKIT=1 docker build -t docker-admin .

docker run -it --privileged --pid=host docker-admin /bin/sh

