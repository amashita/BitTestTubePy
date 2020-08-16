FROM python:3.8-buster

# 日本語が使えるようにする
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get install -y locales
RUN locale-gen ja_JP.UTF-8

ENV LANG ja_JP.UTF-8
ENV LC_CTYPE ja_JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP.utf8

#install google-chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add && \
    echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | tee /etc/apt/sources.list.d/google-chrome.list && \
    apt-get update && \
    apt-get install -y google-chrome-stable

# add user
ARG DOCKER_UID=501
ARG DOCKER_USER=docker
ARG DOCKER_PASSWORD=docker
RUN useradd -m -u ${DOCKER_UID} -G sudo ${DOCKER_USER} \
    && echo ${DOCKER_USER}:${DOCKER_PASSWORD} | chpasswd

# set workdir
WORKDIR /home/${DOCKER_USER}/app

# install eel
RUN pip install -U pip \
    && pip install eel

#set user
USER ${DOCKER_USER}

# not to use shared memory
ENV QT_X11_NO_MITSHM=1
