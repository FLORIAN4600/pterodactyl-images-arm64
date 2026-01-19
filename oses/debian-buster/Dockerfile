FROM debian:buster-slim

ENV DEBIAN_FRONTEND noninteractive

## add container user
RUN useradd -m -d /home/container -s /bin/bash container

RUN ln -s /home/container/ /nonexistent

ENV USER=container HOME=/home/container

## update base packages
RUN echo 'deb [trusted=yes] http://archive.debian.org/debian buster-backports main' > /etc/apt/sources.list \
    && echo 'deb [trusted=yes] http://archive.debian.org/debian-security buster/updates main' >> /etc/apt/sources.list \
    && echo 'deb [trusted=yes] http://archive.debian.org/debian buster main' >> /etc/apt/sources.list \
    && echo 'Acquire::Check-Valid-Until no;' > /etc/apt/apt.conf.d/99no-check-valid-untilRUN apt-get -y update \
    && apt-get -y upgrade

## install dependencies
RUN apt-get -y install curl libjson-c2 gcc g++ libgcc1 libgcc1 libc++-dev gdb libc6 git wget curl tar zip unzip binutils xz-utils liblzo2-2 cabextract iproute2 net-tools netcat-openbsd telnet libatomic1 libsdl1.2debian libsdl2-2.0-0 \
    libfontconfig libicu-dev icu-devtools libunwind8 libssl-dev sqlite3 libsqlite3-dev libmariadbclient-dev libduktape205 locales ffmpeg gnupg2 apt-transport-https ca-certificates tzdata \
    liblua5.3 libz-dev rapidjson-dev

## configure locale
RUN update-locale lang=en_US.UTF-8 \
 && dpkg-reconfigure --frontend noninteractive locales

WORKDIR /home/container

COPY  ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
