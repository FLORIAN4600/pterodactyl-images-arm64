FROM        ghcr.io/florian4600/images:debian-trixie

ENV         DEBIAN_FRONTEND noninteractive

RUN         apt-get update -y \
            && apt-get upgrade -y \
            && apt-get install -y apt-transport-https wget iproute2 \
            && apt-get update -y \
            && apt-get install -y libgdiplus libgssapi-krb5-2 libssl-dev libstdc++6 zlib1g
RUN         apt-get update && apt-get install -y --no-install-recommends libc6 libgcc-s1 libicu-dev libssl-dev tzdata libgdiplus
RUN         wget https://dot.net/v1/dotnet-install.sh \ 
            && chmod +x dotnet-install.sh \
            && mkdir -p /dotnet \
            && ./dotnet-install.sh -c 3.0 -InstallDir /dotnet -Runtime aspnetcore

ENV         DOTNET_ROOT="/dotnet" 
ENV         PATH="/dotnet:${PATH}"

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
