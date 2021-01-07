### Before You Start
This project will help you to run TeamCity 2020.2.1 on your Raspberry Pi 4 Model B.
Might work for older versions of Raspberry Pi as well.
Tested on Ubuntu 20.04.1 LTS.

Navigate to http://<host>:8111 to access Teamcity. There are some remaining steps
that you need to do in the web UI, especially authorizing the build agent.

### Prerequisites for Raspberry Pi
- Docker 19.03.14 (installation instruction for Ubuntu systems)
```
> sudo apt-get remove \
    docker \
    docker-engine \
    docker.io \
    containerd \
    runc
> sudo apt-get update
> sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
> curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
> sudo add-apt-repository \
    "deb [arch=arm64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable"
> sudo apt-get update
> sudo apt-get install docker-ce=5:19.03.14~3-0~ubuntu-$(lsb_release -cs) \
    docker-ce-cli=5:19.03.14~3-0~ubuntu-$(lsb_release -cs) \
    containerd.io
```
- docker-compose 1.27.4
```
> sudo curl \
    -L "https://github.com/linuxserver/docker-docker-compose/releases/download/1.27.4-ls25/docker-compose-arm64" \
    -o /usr/bin/docker-compose
> sudo chmod +x /usr/bin/docker-compose
```

#### Other versions of Docker or docker-compose
I can't guarantee that this project will work for other versions of Docker or docker-compose.

### What does TeamCity support out of the box?
- .NET 5 SDK
- `docker` command
- `docker-compose` command