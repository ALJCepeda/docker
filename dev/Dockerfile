FROM ubuntu:bionic

ARG NODE_VERSION=12.14.0
ENV NODE_VERSION=$NODE_VERSION
ENV NVM_DIR=/root/.nvm
ENV PATH=${NVM_DIR}/versions/node/v${NODE_VERSION}/bin/:$PATH

RUN bash -c '\
  apt-get update &&\
  apt-get -y install curl wget git vim zsh apt-utils &&\
  wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O - | zsh || true &&\
  sed -i "s/ZSH_THEME=.*/ZSH_THEME=\"bira\"/" ~/.zshrc &&\
  echo "source $NVM_DIR/nvm.sh" >> ~/.zshrc &&\
  curl https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash'

RUN bash -c '\
  source $NVM_DIR/nvm.sh &&\
  nvm install $NODE_VERSION &&\
  nvm alias default $NODE_VERSION &&\
  nvm use default'

RUN echo "#!/usr/bin/env bash \n\
  if [ -d "/mnt/.ssh" ] \n\
  then \n\
    mkdir /root/.ssh \n\
    cp /mnt/.ssh/* /root/.ssh \n\
    chmod 0644 /root/.ssh/id_rsa.pub \n\
    chmod 0600 /root/.ssh/id_rsa \n\
    if [ -f "/root/.ssh/known_hosts" ] \n\
    then \n\
      chmod 0644 /root/.ssh/known_hosts \n\
    fi \n\
    if [ -f "/root/.ssh/authorized_keys" ] \n\
    then \n\
      chmod 0600 /root/.ssh/authorized_keys \n\
    fi \n\
  fi \n\
  zsh \n\
" > /dev.entrypoint.sh && chmod +x /dev.entrypoint.sh

VOLUME ["/mnt/host", "/mnt/.ssh"]
WORKDIR /mnt/host
ENTRYPOINT ["/dev.entrypoint.sh"]
