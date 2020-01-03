FROM dev:latest

ARG GIT_URL

RUN echo "#!/usr/bin/env bash\n\
if [ ! -f "/app/package.json" ]\n\
then\n\
  cp -rip /root/app/* /app\n\
fi\n\
/bin/zsh \
" > /root/git.entrypoint.sh

RUN chmod +x /root/git.entrypoint.sh &&\
    git clone ${GIT_URL} /root/app &&\
    cd /root/app

WORKDIR /app
VOLUME ["/app"]
ENTRYPOINT ["/root/git.entrypoint.sh"]
