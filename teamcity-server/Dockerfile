FROM rpi-teamcity_jdk11
LABEL maintainer="Vova Lantsov"
LABEL contact_email="contact@vova-lantsov.dev"
LABEL telegram="https://t.me/vova_lantsov"

RUN curl -SL --output TeamCity.tar.gz https://download.jetbrains.com/teamcity/TeamCity-2020.2.2.tar.gz && \
    tar -xzf TeamCity.tar.gz && \
    rm TeamCity.tar.gz

EXPOSE 8111 9090

ENV TEAMCITY_DATA_PATH /root/BuildServer
ENTRYPOINT ["TeamCity/bin/teamcity-server.sh","run"]