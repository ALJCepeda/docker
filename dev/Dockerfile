FROM ubuntu:bionic

ARG NODE_VERSION=12.14.0
ENV NODE_VERSION=$NODE_VERSION
ENV NVM_DIR=/root/.nvm
ENV PATH=${NVM_DIR}/versions/node/v${NODE_VERSION}/bin/:$PATH

VOLUME ["/mnt/host"]

COPY . .
RUN bash provision.bash

WORKDIR /mnt/host
CMD "/bin/zsh"