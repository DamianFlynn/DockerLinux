#
# couchpotato
#

# sudo docker build -t couchpotato ./docker/couchpotato/.
# sudo docker run --name couchpotato --restart=always -v /opt/couchpotato/config:/CouchPotatoServer/config -v /opt/couchpotato/data:/CouchPotatoServer/data -v /store/downloads:/store/downloads -v /store/media:/store/media -p 8083:5050 -d couchpotato

# configuration      /opt/couchpotato
# Logs               /var/log/couchpotato
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
python-openssl"

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
RUN git clone https://github.com/RuudBurger/CouchPotatoServer.git /CouchPotatoServer

# adding custom files
#ADD config.ini /sickrage/config/config.ini

# set volumes
VOLUME /store/downloads /store/media /CouchPotatoServer/config

# expose ports
EXPOSE 5050

# Launch command
ENTRYPOINT ["/CouchPotatoServer/CouchPotato.py","--config","/CouchPotatoServer/config/config.ini","--data_dir","/CouchPotatoServer/data","--console_log"]

