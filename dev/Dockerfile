FROM ubuntu:bionic

ARG NODE_VERSION=12.14.0
ENV NODE_VERSION=$NODE_VERSION
ENV NVM_DIR=/root/.nvm
ENV PATH=${NVM_DIR}/versions/node/v${NODE_VERSION}/bin/:$PATH

VOLUME ["/mnt/host", "/build"]

COPY . .
RUN bash provision.bash; rm provision.bash

WORKDIR /mnt/host