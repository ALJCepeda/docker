FROM ajrelic/dev:latest

ARG GIT_URL
ARG GIT_BRANCH=dev

RUN echo "#!/usr/bin/env bash\n\
if [ ! -f "/app/package.json" ]\n\
then\n\
  cp -rip /root/app/* /app\ &&\n\
  rm -r /root/app \n\
fi\n\
/bin/zsh \
" > /root/git.entrypoint.sh

RUN bash -c 'chmod +x /root/git.entrypoint.sh &&\
    git clone ${GIT_URL} /root/app &&\
    cd /root/app &&\
    git checkout ${GIT_BRANCH} &&\
    npm ci'

WORKDIR /app
VOLUME ["/app"]
ENTRYPOINT ["/root/git.entrypoint.sh"]
