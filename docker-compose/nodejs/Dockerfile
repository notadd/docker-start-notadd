FROM node:10-alpine

ARG GIT_ADDRESS=${GIT_ADDRESS}

ARG GIT_KEY=${GIT_KEY}

# 同步时区，安装 git

RUN apk --no-cache add tzdata ca-certificates git openssh-client&& \
    cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    mkdir -p /root/.ssh && \
    echo -e "Host *\n\tStrictHostKeyChecking no\n" >>/root/.ssh/config && echo "nameserver 119.29.29.29" >>/etc/resolv.conf && \
    yarn cache clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm /var/cache/apk/*

## git 从仓库同步代码

RUN   mkdir -p /root/.ssh && echo -e "${GIT_KEY}" > /root/.ssh/id_rsa && chmod 600 /root/.ssh/id_rsa && \
      git clone ${GIT_ADDRESS}  /var/www && \
      mv /app/node_modules /var/www/ && \
      rm -rf /var/www/.git && \
      apk del git openssh-client

## yarn install

RUN apk update && apk add --no-cache --virtual .fetch-deps \
    python2 \
    make \
    g++ \
    gcc && \
    yarn install && \
    apk del .fetch-deps

CMD ["yarn", "start"]