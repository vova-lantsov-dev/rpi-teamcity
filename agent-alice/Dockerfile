FROM rpi-teamcity_server
LABEL maintainer="uPagge"
LABEL contact_email="upagge@mail.ru"
LABEL telegram="https://t.me/uPagge"

ADD buildAgent.properties TeamCity/buildAgent/conf/

RUN apt-get install -y git curl zlib1g liblttng-ust0 apt-transport-https gnupg-agent software-properties-common
RUN apt-get upgrade -y

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

RUN add-apt-repository \
   "deb [arch=arm64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

RUN apt-get update
RUN apt-get install docker-ce=5:19.03.14~3-0~debian-bullseye docker-ce-cli=5:19.03.14~3-0~debian-bullseye containerd.io

RUN apt-get upgrade -y

EXPOSE 8111 9090
ENTRYPOINT TeamCity/buildAgent/bin/agent.sh run