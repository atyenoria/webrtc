#docker run -it --restart="on-failure:10"  -v $(pwd)/coturn:/coturn --net=host -p 3478:3478 -p 3478:3478/udp coturn bash
FROM phusion/baseimage:0.9.16
MAINTAINER Carl Kittelberger <icedream2k9@die-optimisten.net>

# Set correct environment variables.
ENV HOME /root

# Use baseimage-docker's init system.

RUN apt-get update && apt-get dist-upgrade -y
RUN apt-get install -y gdebi-core

ENV COTURN_VER 4.4.5.3
RUN cd /tmp/ && curl -sL http://turnserver.open-sys.org/downloads/v${COTURN_VER}/turnserver-${COTURN_VER}-debian-wheezy-ubuntu-mint-x86-64bits.tar.gz | tar -xzv

RUN groupadd turnserver
RUN useradd -g turnserver turnserver
RUN gdebi -n /tmp/coturn*.deb

RUN mkdir /etc/service/turnserver
ADD turnserver.sh /etc/service/turnserver/run
RUN chmod +x /etc/service/turnserver/run

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /tmp
# CMD ["/sbin/my_init"]
CMD ["bash"]

