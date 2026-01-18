FROM        ghcr.io/florian4600/images:debian

RUN         apt update \
            && apt -y upgrade
RUN         apt install -y fontconfig dirmngr
RUN         wget -O- "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" | gpg --dearmor | tee /etc/apt/trusted.gpg.d/nondudepot.gpg > /dev/null
RUN         sh -c 'echo "deb https://download.mono-project.com/repo/debian stable-trixie/snapshots/5.14.0.177 main" > /etc/apt/sources.list.d/mono-official-stable.list'
RUN         apt update
RUN         apt install -y mono-complete

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]