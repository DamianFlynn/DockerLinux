#
# sabnzbd
#

# sudo docker build -t sabnzbd ./docker/sabnzbd/.
# sudo docker run --name sabnzbd --restart=always --net=host -d sabnzbd

FROM phusion/baseimage:0.9.18
MAINTAINER Damian Flynn <info@damianflynn.com>

ENV DEBIAN_FRONTEND noninteractive

ENV APTLIST="sabnzbdplus \
sabnzbdplus-theme-mobile \
sabnzbdplus-theme-classic \
sabnzbdplus-theme-plush \
python-yenc \
unzip \
unrar \
wget"

# Set the locale
ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8
RUN locale-gen en_US.UTF-8

# add new repositories
RUN add-apt-repository ppa:jcfp/ppa

# Install multithreaded par2
#RUN apt-get remove --purge -y par2 && \
#    wget -P /tmp http://www.chuchusoft.com/par2_tbb/par2cmdline-0.4-tbb-20141125-lin64.tar.gz && \
#    tar -C /usr/local/bin -xvf /tmp/par2cmdline-0.4-tbb-20141125-lin64.tar.gz --strip-components 1

# install main packages
RUN apt-get update -q && \
    apt-get install $APTLIST -qy --force-yes && \
    apt-get autoremove -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


# set volumes
VOLUME /config /store/downloads

# expose ports
EXPOSE 8082 9090

# Launch command
CMD ["/usr/bin/sabnzbdplus","--config-file","/config","--console"]
