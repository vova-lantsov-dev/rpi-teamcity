FROM rpi-teamcity_jdk11
LABEL maintainer="pixelistik"
LABEL contact_email="code@pixelistik.de"

RUN wget -v https://download.jetbrains.com/teamcity/TeamCity-2020.2.1.tar.gz && \
    tar -xzvf TeamCity-2020.2.1.tar.gz && \
    rm TeamCity-2020.2.1.tar.gz

EXPOSE 8111 9090

ENV TEAMCITY_DATA_PATH /root/BuildServer
ENTRYPOINT ["TeamCity/bin/teamcity-server.sh","run"]