#
# oscam
#

# sudo docker build -t oscam ~/docker/oscam/
# sudo docker run --name oscam --restart=always -v /opt/oscam:/oscam/config  --device=/dev/ttyUSB0 --device=/dev/ttyUSB1 -p 8000:8000 -p 9000:9000 -d oscam
# sudo docker run -it oscam /bin/bash

# Configuration      /opt/oscam
# Music Media        /store/media/music/

#FROM phusion/baseimage:0.9.18
FROM ubuntu:15.10
MAINTAINER Damian Flynn <info@damianflynn.com>

ENV DEBIAN_FRONTEND noninteractive

ENV APTLIST="python-cheetah \
python-pip \
build-essential \
git-core \
python-dev \
python-openssl \
libpcsclite-dev \
libssl-dev \
libusb-dev \
libusb-1.0 \
usbutils \
openssl \
subversion \
libpcsclite1 \
pcscd \
pcsc-tools \
usbutils"

# Set the locale
ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8
RUN locale-gen en_US.UTF-8


# install main packages
RUN apt-get update -q && \
    apt-get install $APTLIST -qy --force-yes --no-install-recommends && \
    apt-get autoremove -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Grab the Code from its GIT Repostitory
RUN svn checkout http://www.streamboard.tv/svn/oscam/trunk /oscam

RUN cd /   && \
    cd oscam  && \
    ./config.sh --enable all --disable LCDSUPPORT LEDSUPPORT READ_SDT_CHARSETS  && \
    make OSCAM_BIN=/usr/bin/oscam NO_PLUS_TARGET=1 CONF_DIR=/oscam/config pcsc-libusb

# adding custom files
#ADD config.ini /sickrage/config/config.ini

COPY config /oscam/config

# set volumes
VOLUME /oscam/config

# expose ports
EXPOSE 8000 9000

# Launch command
#ENTRYPOINT ["/sickrage/SickBeard.py","--config","/sickrage/config/config.ini"]
ENTRYPOINT ["/usr/bin/oscam"]
#CMD ["/usr/bin/sabnzbdplus","--config-file","/config","--console"]
#CMD ["/bin/bash"]
