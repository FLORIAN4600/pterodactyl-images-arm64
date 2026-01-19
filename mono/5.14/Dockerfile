FROM        ghcr.io/florian4600/images:debian-stretch

RUN         apt update \
            && apt -y upgrade
RUN         apt install -y fontconfig dirmngr
RUN         sh -c 'echo "deb [trusted=yes] https://download.mono-project.com/repo/debian stable-jessie/snapshots/5.14.0.177 main" > /etc/apt/sources.list.d/mono-official-stable.list'
RUN         apt update
RUN         apt install -y mono-complete

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]