FROM ajrelic/dev:latest

ARG GIT_URL
ARG GIT_BRANCH=dev

RUN bash -c 'git clone ${GIT_URL} /root/repo &&\
  cd /root/repo &&\
  git checkout ${GIT_BRANCH} &&\
  npm ci'

RUN echo "#!/usr/bin/env bash \n\
if [ ! -f "/mnt/host/package.json" ] \n\
then \n\
  setopt -s glob_dots \n\
  mv /root/repo/* /mnt/host \n\
fi \n\
zsh \n\
" > /git.entrypoint.sh &&\
  chmod +x /git.entrypoint.sh

EXPOSE 3000
EXPOSE 80

ENTRYPOINT ["/git.entrypoint.sh"]
