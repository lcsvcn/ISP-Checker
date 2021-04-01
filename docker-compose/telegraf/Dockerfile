FROM telegraf:latest

ARG ARCH

LABEL mantainer="Facu de la Cruz"
LABEL email="fmdlc.unix@gmail.com"
LABEL project="ISP-Checker"
LABEL component="telegraf"

COPY ./bin/entrypoint.sh /entrypoint.sh

RUN apt-get install gnupg1 apt-transport-https dirmngr \
    export INSTALL_KEY=379CE192D401AB61 \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys $INSTALL_KEY \
    echo "deb https://ookla.bintray.com/debian generic main" | sudo tee  /etc/apt/sources.list.d/speedtest.list \
    apt-get update && apt-get install -y --no-install-recommends \
    apt-get install mtr \
    apt-get install speedtest && \
    rm -rf /var/lib/apt/lists/* && \
    usermod -G video telegraf

EXPOSE 8125/udp 8092/udp 8094

ENTRYPOINT ["/entrypoint.sh"]

CMD ["telegraf"]
