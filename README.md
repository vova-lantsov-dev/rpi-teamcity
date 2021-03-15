### Before You Start
This project will help you to run TeamCity 2020.2 on your Raspberry Pi 4 Model B.
Tested on Ubuntu 20.04.1 LTS.

Navigate to `http://<host>:8111` to access Teamcity. There are some remaining steps
that you need to do in the web UI, especially authorizing the build agent.

### Prerequisites for Raspberry Pi
- Docker 20.10.5 (or similar version)
- docker-compose 1.28.5
```
> sudo curl \
    -L "https://github.com/linuxserver/docker-docker-compose/releases/download/1.28.5-ls33/docker-compose-arm64" \
    -o /usr/bin/docker-compose
> sudo chmod +x /usr/bin/docker-compose
```

### What is supported by TeamCity agent?
| Tool Name | Tool Version | Description | End of support |
| --------- | ------------ | ----------- | -------------- |
| .NET Core 2.1 SDK | v2.1.26 (SDK 2.1.814) | Long-term support release.<br>**Included runtimes:**<br>.NET Core Runtime 2.1.26<br>ASP.NET Core Runtime 2.1.26 | 2021-08-21 |
| .NET Core 3.1 SDK | v3.1.13 (SDK 3.1.407) | Long-term support release.<br>**Included runtimes:**<br>.NET Core Runtime 3.1.13<br>ASP.NET Core Runtime 3.1.13 | 2022-12-03 |
| .NET 5 SDK | v5.0.4 (SDK 5.0.201) | **Included runtimes:**<br>.NET Runtime 5.0.4<br>ASP.NET Core Runtime 5.0.4 | N/A |
| docker-compose | 1.28.5 | Compose is a tool for defining and running multi-container Docker applications.<br>With Compose, you use a YAML file to configure your application's services. | N/A |
| docker | 20.10.5 | Docker provides the ability to package and run an application in a loosely isolated environment called a container.<br>The isolation and security allow you to run many containers simultaneously on a given host. | N/A |
