#
# sickrage
#

# sudo docker build -t sickrage ./docker/sickrage/.
# sudo docker run --name sickrage --restart=always -v /opt/sickrage:/sickrage/config -v /var/log/sickrage:/sickrage/Logs -v /store/downloads:/store/downloads -v /store/media:/store/media -p 8082:8081 -d sickrage

# configuration      /opt/sickrage
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
#RUN git clone https://github.com/SiCKRAGETV/SickRage.git sickrage
RUN git clone https://github.com/SickRage/SickRage.git sickrage

# adding custom files
ADD config.ini /sickrage/config/config.ini

# set volumes
VOLUME /store/downloads /store/media /sickrage/config /sickrage/Logs

# expose ports
EXPOSE 8081

# Launch command
#ENTRYPOINT ["/sickrage/SickBeard.py","--config","/sickrage/config/config.ini"]
ENTRYPOINT ["/sickrage/SickBeard.py","--datadir","/sickrage/config"]
#CMD ["/usr/bin/sabnzbdplus","--config-file","/config","--console"]

