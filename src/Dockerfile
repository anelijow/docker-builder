FROM buildpack-deps:jessie

MAINTAINER Kristoffer Richardsson <kristoffer@bitcraze.io>

RUN dpkg --add-architecture i386 && apt-get update \
    && apt-get install -y --no-install-recommends \
		telnet \
		libncurses5:i386 \
		zip unzip \
		sdcc libftdi-dev \
		python python-pip python-wheel python-dev \
		python3 python3-pip python3-wheel python3-dev \
		rake \
		python-numpy python-scipy python3-numpy python3-scipy \
	&& rm -rf /var/lib/apt/lists/*

RUN curl -fsSLO https://launchpad.net/gcc-arm-embedded/5.0/5-2016-q2-update/+download/gcc-arm-none-eabi-5_4-2016q2-20160622-linux.tar.bz2 \
    && tar --strip-components=1 -xvjf gcc-arm-none-eabi-5_4-2016q2-20160622-linux.tar.bz2 -C /usr/local/

ENV DOCKER_VERSION 1.12.0
RUN curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz && tar --strip-components=1 -xvzf docker-1.12.0.tgz -C /usr/local/bin

RUN pip2 install flake8 pyusb==1.0.0b2 mock
RUN pip3 install flake8 pyusb==1.0.0b2

RUN pip3 install pre-commit
# Make pre-commit donwload and prepare all tools
ADD .pre-commit-config.yaml /dummy/.pre-commit-config.yaml
RUN cd /dummy && git init && pre-commit run && cd && rm -rf /dummy

WORKDIR /module
