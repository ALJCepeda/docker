FROM ajrelic/dev:latest

ARG GIT_URL
ARG GIT_BRANCH=dev

RUN echo "#!/usr/bin/env bash\n\
if [ ! -f "/repo/package.json" ]\n\
then\n\
  setopt -s glob_dots \n\
  mv /root/repo/* /repo \n\
fi\n\
/bin/zsh \
" > /root/git.entrypoint.sh

RUN bash -c 'chmod +x /root/git.entrypoint.sh &&\
    git clone ${GIT_URL} /root/repo &&\
    cd /root/repo &&\
    git checkout ${GIT_BRANCH} &&\
    npm ci'

WORKDIR /repo
VOLUME ["/repo"]
ENTRYPOINT ["/root/git.entrypoint.sh"]
