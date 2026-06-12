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
RUN adduser -D admin

EXPOSE 3000

RUN npm install -g pm2

# mkdir www
RUN mkdir -p /home/admin/www
RUN chown -R admin:admin /home/admin
RUN chown -R admin:admin /usr/local/share/corepack

USER admin

# Switch To target Directory
WORKDIR /home/admin/www

# Let's make os more colorful
RUN bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"

COPY ./.bashrc /home/admin/.bashrc
COPY ./robbyrussell.theme.sh /home/admin/.oh-my-bash/themes/robbyrussell

# Prep PM2 logs
RUN mkdir /home/admin/.pm2
RUN mkdir /home/admin/.pm2/logs

CMD  ["top"]
