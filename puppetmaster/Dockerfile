###########################################################
# Dockerfile to build container image of Puppet
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

# Install Puppet Master Server
RUN apt-get install -y wget && \
    apt-get install -y elinks && \
    apt-get install -y nano && \
    apt-get install -y telnet && \
    wget https://apt.puppetlabs.com/puppetlabs-release-trusty.deb &&\ 
    dpkg -i puppetlabs-release-trusty.deb &&\
    apt-get update &&\
    apt-get -y install puppetmaster

# Chanaging puppet master conf file to fix pupet version
RUN sed -i '7 s/^/#/' /etc/puppet/puppet.conf &&\
	echo -e "# /etc/apt/preferences.d/00-puppet.pref\nPackage: puppet puppet-common puppetmaster-passenger\nPin: version 3.7*\nPin-Priority: 501">/etc/apt/preferences.d/00-puppet.pref

# Changing puppet conf file for certname
RUN sed -i '2 a certname = puppet' /etc/puppet/puppet.conf &&\
	sed -i '3 a dns_alt_names = puppet,puppetmaster.com' /etc/puppet/puppet.conf

# Set Puppet Certificates
RUN rm -rf /var/lib/puppet/ssl &&\
    puppet master --verbose &&\
    touch /etc/puppet/manifests/site.pp
ENTRYPOINT service puppetmaster start && bash