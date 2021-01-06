This project will help you to run TeamCity 2020.2.1 on your Raspberry Pi 4 Model B. Might work for older versions of Raspberry Pi.

Before starting, install docker-compose.

Open http://<host>:8111 to access Teamcity. There are some remaining steps
that you need to do in the web UI, especially authorizing the build agent.

### Troubleshooting
While using the Docker 20+ version, you might get a warning:
```
[Warning] The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
```
If it happens, downgrade to the latest stable version of Docker: 19.03.14 (instruction: https://docs.docker.com/engine/install/ubuntu/#install-docker-engine)