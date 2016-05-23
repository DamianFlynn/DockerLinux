#
# sabnzbd
#

# sudo docker build -t sabnzbd ./docker/sabnzbd/.
# sudo docker run --name sabnzbd --restart=always --net=host -d sabnzbd
FROM tcnksm/centos-ruby
MAINTAINER Damian Flynn <info@damianflynn.com>

WORKDIR	/root

RUN	ruby -S gem install jekyll therubyracer

EXPOSE	4000
