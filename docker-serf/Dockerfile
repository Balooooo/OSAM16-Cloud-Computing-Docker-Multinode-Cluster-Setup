# Creates a base ubuntu image with serf and dnsmasq
#
# The docker images was taken from sequenceiq and converetd to ubuntu image

FROM ubuntu:12.04
MAINTAINER Jinwoo Chung

RUN apt-get update
RUN apt-get -y install dnsmasq
RUN apt-get -y install git

# dnsmasq configuration
ADD dnsmasq.conf /etc/dnsmasq.conf
ADD resolv.dnsmasq.conf /etc/resolv.dnsmasq.conf

# install serfdom.io
RUN git clone https://github.com/hashicorp/serf.git /tmp

ENV SERF_CONFIG_DIR /etc/serf

# configure serf
ADD serf-config.json $SERF_CONFIG_DIR/serf-config.json

ADD event-router.sh $SERF_CONFIG_DIR/event-router.sh
RUN chmod +x  $SERF_CONFIG_DIR/event-router.sh

ADD handlers $SERF_CONFIG_DIR/handlers

ADD start-serf-agent.sh  $SERF_CONFIG_DIR/start-serf-agent.sh
RUN chmod +x  $SERF_CONFIG_DIR/start-serf-agent.sh

EXPOSE 7373 7946

CMD /etc/serf/start-serf-agent.sh
