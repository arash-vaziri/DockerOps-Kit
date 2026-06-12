FROM node:24-alpine

# 1. Define a shared system cache directory for Corepack
ENV COREPACK_HOME=/usr/local/share/corepack

# Git
RUN apk add git

# add curl for oh my bash
RUN apk add curl

#Handle Timezone properly
RUN apk add -U tzdata
ENV TZ=Asia/Kuala_Lumpur

# add bash
RUN apk add bash
RUN apk add bash-doc
RUN apk add bash-completion

# updated yarn
RUN corepack enable
RUN corepack install --global yarn@4.15.0

# add task for easier task management
RUN apk add --no-cache bash go-task \
  && ln -s /usr/bin/go-task /usr/local/bin/task

# add admin user
# RUN adduser -D admin

EXPOSE 3000

# RUN yarn global add pm2

# mkdir www
RUN cd /home/node/
RUN mkdir www
RUN chown -R node:node /home/node
RUN chown -R node:node /usr/local/share/corepack

USER node

# Switch To target Directory
WORKDIR /home/node/www

# Let's make os more colorful
RUN bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"

COPY ./.bashrc /home/node/.bashrc
COPY ./robbyrussell.theme.sh /home/node/.oh-my-bash/themes/robbyrussell

# Prep PM2 logs
# RUN mkdir /home/admin/.pm2
# RUN mkdir /home/admin/.pm2/logs

CMD  ["top"]