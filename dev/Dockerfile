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

VOLUME ["/mnt/host"]
WORKDIR /mnt/host
CMD ["/bin/zsh"]
