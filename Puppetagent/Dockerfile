###########################################################
# Dockerfile to build container image of Puppet-Agent
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM vigneswaranauto/ubuntu:14.04
ENV DEBIAN_FRONTEND noninteractive

# File Author / Maintainer
MAINTAINER vigneswaran (vigneswaranauto@gamil.com)
RUN mkdir /puppet
WORKDIR /puppet

# Update the repository sources list
RUN apt-get update

# Install NTP service for time sync
RUN apt-get -y install ntp &&\
    service ntp restart

# Adding puppet master entry to hosts file
RUN echo "172.17.0.2   puppet" >> /etc/hosts

# Install Puppet Master Server
RUN apt-get install -y wget && \
    apt-get install -y elinks && \
    apt-get install -y nano && \
    apt-get install -y telnet && \
    wget https://apt.puppetlabs.com/puppetlabs-release-trusty.deb &&\ 
    dpkg -i puppetlabs-release-trusty.deb &&\
    apt-get update &&\
    apt-get -y install puppet

# Chanaging puppet master conf file to fix pupet version
RUN sed -i '7,13 s/^/#/' /etc/puppet/puppet.conf &&\
	echo -e "# /etc/apt/preferences.d/00-puppet.pref\nPackage: puppet puppet-common puppetmaster-passenger\nPin: version 3.7*\nPin-Priority: 501">/etc/apt/preferences.d/00-puppet.pref

# Changing puppet conf file for certname
RUN echo "[agent]" >> /etc/puppet/puppet.conf &&\
	echo "server = puppet" >> /etc/puppet/puppet.conf 

# Enabling agent run conf file
RUN sed -i s/START\=no/START\=yes/g /etc/default/puppet

ENTRYPOINT service puppet start && bash