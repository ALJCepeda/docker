FROM ajrelic/dev:latest

ARG GIT_URL
ARG GIT_BRANCH=dev

RUN echo "#!/usr/bin/env bash\n\
if [ ! -f "/app/package.json" ]\n\
then\n\
  mv /root/repo /documents \n\
fi\n\
/bin/zsh \
" > /root/git.entrypoint.sh

RUN bash -c 'chmod +x /root/git.entrypoint.sh &&\
    git clone ${GIT_URL} /root/repo &&\
    cd /root/repo &&\
    git checkout ${GIT_BRANCH} &&\
    npm ci'

WORKDIR /documents/repo
VOLUME ["/documents/repo"]
ENTRYPOINT ["/root/git.entrypoint.sh"]
