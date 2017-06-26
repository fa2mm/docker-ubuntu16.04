FROM fa2m/ubuntu16.04

MAINTAINER fa2m

# install Golang
RUN cd ~ \
    && curl -O https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.8.3.linux-amd64.tar.gz

# start as ubuntu (user)
USER ubuntu

# setting variables for ubuntu
ENV PATH="${PATH}:/usr/local/go/bin"

USER root

