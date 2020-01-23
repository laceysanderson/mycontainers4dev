FROM node:stretch

MAINTAINER Lacey-Anne Sanderson <laceyannesanderson@gmail.com>

## This image is focused on exploring JBrowse2 web version.

EXPOSE 3000

WORKDIR /home/node/app

RUN git clone https://github.com/GMOD/jbrowse-components.git \
  && cd jbrowse-components && yarn
