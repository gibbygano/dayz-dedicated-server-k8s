# Ubuntu noble can kiss my ass
FROM steamcmd/steamcmd:ubuntu-jammy

# install deps
RUN useradd -m steam \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y apt-utils \
    && apt-get install -y \
        lib32gcc-s1 \
        libcap-dev \
        libcurl4 \
        libcurl4-openssl-dev \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*

USER steam

ENV USER=steam
ENV HOME=/home/steam
ENV GAME=dayz
ENV APPID=223350
ENV STEAMACCOUNT=anonymous
ENV STEAMPASSWORD=
ENV MODS=
ENV CPUCOUNT=2
ENV PORT=2302

WORKDIR /home/steam

# permissions
RUN mkdir ${HOME}/${GAME} && \
    mkdir ${HOME}/profile && \
    mkdir ${HOME}/battleye && \
    chown -R steam ${HOME}

# Exposed Ports
# game
EXPOSE ${PORT}/udp
EXPOSE 2302/udp
EXPOSE 2303/udp
EXPOSE 2304/udp
EXPOSE 2305/udp
# steam
EXPOSE 8766/udp
EXPOSE 27016/udp
# rcon
EXPOSE 2310

# update steamcmd
RUN steamcmd +quit

# define entrypoint
COPY entry.sh ${HOME}/entry.sh

ENTRYPOINT "${HOME}/entry.sh"
