FROM ubuntu:16.04

MAINTAINER fa2m

## Ubuntu 16.04 settings ##

# update system
RUN apt -y update \
    && apt -y upgrade

# install tools
RUN apt -y install \
    sudo \
    vim \
    curl \
    unzip \
    tar \
    mc \
    htop

# create new user (username:password)
RUN useradd -m -s /bin/bash ubuntu \
    && echo 'ubuntu:ubuntu' | chpasswd \
    && gpasswd -a ubuntu sudo

