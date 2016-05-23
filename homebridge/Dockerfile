#
# airsonos
#

# sudo docker build -t homebridge ./docker/homebridge/.
# sudo docker run --name homebridge --restart=always -v /opt/homebridge:/root/.homebridge -p 8082:8081 -d homebridge

# configuration      /opt/homebridge
# Logs               /var/log/sickrage
# Completed Download /store/downloads/completed
# TV Media           /store/media/video/tv
# Movie Media        /store/media/video/movies
# Music Media        /store/media/music/

FROM phusion/baseimage:0.9.18
MAINTAINER Damian Flynn <info@damianflynn.com>

ENV DEBIAN_FRONTEND noninteractive

ENV APTLIST="python-cheetah \
python-pip \
build-essential \
git-core \
python-dev \
python-openssl \
libavahi-compat-libdnssd-dev \
libasound2-dev \
nodejs"

# Set the locale
ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8
RUN locale-gen en_US.UTF-8

# Using Debian, as root register Node 0.12 repo
# see https://github.com/nodesource/distributions
#RUN curl -sL https://deb.nodesource.com/setup_0.12 | bash -
RUN curl -sl https://deb.nodesource.com/setup_4.x | bash -

# install main packages
RUN apt-get update -q && \
    apt-get install $APTLIST -qy --force-yes --no-install-recommends && \
    apt-get autoremove -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Grab the Code from its GIT Repostitory
RUN git clone https://github.com/nfarina/homebridge /homebridge
RUN npm install -g babel
RUN cd /homebridge && \
    sudo npm install -g


# adding custom files
#ADD config.ini /sickrage/config/config.ini

# set volumes
VOLUME /root/.homebridge

# expose ports
EXPOSE 5000 5001 5002 5003 5004 5005 5006 5006 5007 5008 5009 5010 5011 5012 5013 5014 5015

# Launch command
#ENTRYPOINT ["/sickrage/SickBeard.py","--config","/sickrage/config/config.ini"]
#CMD ["/usr/bin/sabnzbdplus","--config-file","/config","--console"]

