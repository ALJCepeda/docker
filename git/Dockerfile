FROM ajrelic/dev:latest

ARG GIT_URL
ARG GIT_BRANCH=dev

RUN bash -c 'git clone ${GIT_URL} /root/repo &&\
    cd /root/repo &&\
    git checkout ${GIT_BRANCH} &&\
    npm ci'

EXPOSE 3000
EXPOSE 80
EXPOSE 9222
EXPOSE 9229

WORKDIR /repo
VOLUME ["/repo"]

RUN echo "#!/usr/bin/env bash\n\
if [ ! -f "/repo/package.json" ]\n\
then\n\
  setopt -s glob_dots \n\
  mv /root/repo/* /repo \n\
  zsh \n\
fi\n\
" > /git.entrypoint.sh &&\
  chmod +x /root/git.entrypoint.sh

ENTRYPOINT ["/git.entrypoint.sh"]
