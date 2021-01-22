# Based on https://github.com/balena-io-library/base-images/blob/master/balena-base-images/dotnet/aarch64/debian/bullseye/5.0-sdk/run/Dockerfile
# But supports multiple .NET Core SDKs

FROM balenalib/aarch64-debian:bullseye-run
LABEL maintainer="Vova Lantsov"
LABEL contact_email="contact@vova-lantsov.dev"
LABEL telegram="https://t.me/vova_lantsov"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        \
# .NET Core dependencies
        libc6 \
        libgcc1 \
        libgssapi-krb5-2 \
        libicu67 \
        libssl1.1 \
        libstdc++6 \
        zlib1g \
    && rm -rf /var/lib/apt/lists/*

# Configure web servers to bind to port 80 when present
ENV ASPNETCORE_URLS=http://+:80 \
    # Enable detection of running in a container
    DOTNET_RUNNING_IN_CONTAINER=true

# Install .NET Core 2.1 SDK
ENV DOTNET_2_1_SDK_VERSION 2.1.812
RUN curl -SL --output dotnet.tar.gz "https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_2_1_SDK_VERSION/dotnet-sdk-$DOTNET_2_1_SDK_VERSION-linux-arm64.tar.gz" \
    && dotnet_sha512='e11d5d407008087d90e21ad593fcfc7b2edf7e92221bffeb44597725b88724fd301ff351a52dfeede49b229cd871b719f60d0d0f72c27f1ed895fc4a0fae051b' \
    && echo "$dotnet_sha512 dotnet.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz

# Install .NET Core 3.1 SDK
ENV DOTNET_3_1_SDK_VERSION 3.1.405
RUN curl -SL --output dotnet.tar.gz "https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_3_1_SDK_VERSION/dotnet-sdk-$DOTNET_3_1_SDK_VERSION-linux-arm64.tar.gz" \
    && dotnet_sha512='e720b7c6497da52ce4a927b1a29df5c180fbf5b4f800185de61a31092c0bfa18a78bb9c2fee744fabc78214c5be6e9277f3dc14ae1426b55274f9726997fc733' \
    && echo "$dotnet_sha512 dotnet.tar.gz" | sha512sum -c - \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz

# Install .NET 5 SDK
ENV DOTNET_5_SDK_VERSION 5.0.102
RUN curl -SL --output dotnet.tar.gz "https://dotnetcli.blob.core.windows.net/dotnet/Sdk/$DOTNET_5_SDK_VERSION/dotnet-sdk-$DOTNET_5_SDK_VERSION-linux-arm64.tar.gz" \
    && dotnet_sha512='031272b86f435f88963b560c14342635d892345ac9a35d59ecaf6e425de8aab15ca5c3d0685c79027364e7a323927ba90568fe7ed8610f52ee5f961aef9fcf72' \
    && echo "$dotnet_sha512 dotnet.tar.gz" | sha512sum -c - \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet

# Configure web servers to bind to port 80 when present
# Enable correct mode for dotnet watch (only mode supported in a container)
ENV DOTNET_USE_POLLING_FILE_WATCHER=true \
    # Skip extraction of XML docs - generally not useful within an image/container - helps performance
    NUGET_XMLDOC_MODE=skip

# Trigger first run experience by running arbitrary cmd to populate local package cache
RUN dotnet help

CMD ["echo","'No CMD command was set in Dockerfile! Details about CMD command could be found in Dockerfile Guide section in our Docs. Here's the link: https://balena.io/docs"]

 RUN curl -SLO "https://raw.githubusercontent.com/balena-io-library/base-images/8accad6af708fca7271c5c65f18a86782e19f877/scripts/assets/tests/test-stack@dotnet.sh" \
  && echo "Running test-stack@dotnet" \
  && chmod +x test-stack@dotnet.sh \
  && bash test-stack@dotnet.sh \
  && rm -rf test-stack@dotnet.sh 

RUN [ ! -d /.balena/messages ] && mkdir -p /.balena/messages; echo 'Here are a few details about this Docker image (For more information please visit https://www.balena.io/docs/reference/base-images/base-images/): \nArchitecture: ARM v8 \nOS: Debian Bullseye \nVariant: run variant \nDefault variable(s): UDEV=off \nThe following software stack is preinstalled: \ndotnet 5.0-sdk \nExtra features: \n- Easy way to install packages with `install_packages <package-name>` command \n- Run anywhere with cross-build feature  (for ARM only) \n- Keep the container idling with `balena-idle` command \n- Show base image details with `balena-info` command' > /.balena/messages/image-info

RUN echo '#!/bin/sh.real\nbalena-info\nrm -f /bin/sh\ncp /bin/sh.real /bin/sh\n/bin/sh "$@"' > /bin/sh-shim \
	&& chmod +x /bin/sh-shim \
	&& cp /bin/sh /bin/sh.real \
	&& mv /bin/sh-shim /bin/sh