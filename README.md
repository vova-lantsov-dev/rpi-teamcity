### Before You Start
This project will help you to run TeamCity 2020.2.1 on your Raspberry Pi 4 Model B.
Might work for older versions of Raspberry Pi as well.
Tested on Ubuntu 20.04.1 LTS.

Navigate to `http://<host>:8111` to access Teamcity. There are some remaining steps
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

### What is supported by TeamCity agent?
| Tool Name | Tool Version | Description | End of support |
| --------- | ------------ | ----------- | -------------- |
| .NET Core 2.1 SDK | v2.1.25 (SDK 2.1.813) | Long-term support release.<br>**Included runtimes:**<br>.NET Core Runtime 2.1.25<br>ASP.NET Core Runtime 2.1.25 | 2021-08-21 |
| .NET Core 3.1 SDK | v3.1.12 (SDK 3.1.406) | Long-term support release.<br>**Included runtimes:**<br>.NET Core Runtime 3.1.12<br>ASP.NET Core Runtime 3.1.12 | 2022-12-03 |
| .NET 5 SDK | v5.0.3 (SDK 5.0.103) | **Included runtimes:**<br>.NET Runtime 5.0.3<br>ASP.NET Core Runtime 5.0.3 | N/A |
| docker-compose | 1.27.4 | Compose is a tool for defining and running multi-container Docker applications.<br>With Compose, you use a YAML file to configure your application's services. | N/A |
| docker | 19.03.14 | Docker provides the ability to package and run an application in a loosely isolated environment called a container.<br>The isolation and security allow you to run many containers simultaneously on a given host. | N/A |
