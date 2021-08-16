# docker build

```
git clone git@github.com:jiashunzheng/docker-bitcoin-dev.git
docker build -t tc .
``` 

# use the docker image to compile
假定timecoin代码库已经下载到~/timecoin
```
#进入docker交互模式,将timecoin代码库映射到docker容器中/bitcoin目录
docker run -ti -v ~/timecoin:/bitcoin tc
#指定qt版本
export QT_SELECT="qt5"
qmake
make
```

# 以下内容来自cdecker/docker-bitcoin-dev

# bitcoin-dev Docker Images

Building and developing Bitcoin in docker containers.

# Requirements

* Docker 1.2+
* An X11 socket (for IDEs)

# Images

* [cdecker/bitcoin-dev:common](https://registry.hub.docker.com/u/cdecker/bitcoin-dev/) an image containing all the build dependencies required to build bitcoin from source.
* [cdecker/bitcoin-dev:netbeans](https://registry.hub.docker.com/u/cdecker/bitcoin-dev/) an image with netbeans C++ tools (inspired by [fgrehm/docker-netbeans](https://registry.hub.docker.com/u/fgrehm/netbeans/)).

# Quickstart
In order to build bitcoin in cdecker/bitcoin-dev:common

```
git clone https://github.com/bitcoin/bitcoin.git
sudo docker run -ti -v `pwd`/bitcoin:/bitcoin cdecker/bitcoin-dev:common
./autogen.sh
./configure
make
```
Notice: the last steps are executed in the docker container and are part of the bitcoin build process.

To run netbeans on a checked out copy of the bitcoin sources execute

```
xhost +
sudo docker run -ti \
    -v `pwd`/bitcoin:/bitcoin \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -e DISPLAY=$DISPLAY \
    bitcoin-dev:netbeans
```

Notice that this gives the container access to the host's X server.
