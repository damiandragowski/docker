FROM debian:stable

MAINTAINER Damian Drągowski <damian.dragowski@gmail.com>

RUN apt-get update && apt-get install bc wget unzip openjdk-7-jre curl lib32z1 bc lib32ncurses5 lib32stdc++6 lib32z1 lib32z1-dev -y &&\ 
	groupadd -r tibco -g 433 && \
	useradd -u 431 -r -m -g tibco -d /home/tibusr -s /bin/bash -c "tibco user" tibusr && \
	chown -R tibusr:tibco /home/tibusr && \
	mkdir /opt/tibco && \
	chown -R tibusr:tibco /opt/tibco && \
	mkdir /tmp/install && \
	chown -R tibusr:tibco /tmp/install
	
RUN mkdir -p /tmp/install && \
    cd /tmp/install && \
    wget --quiet https://edownloads.tibco.com/Installers/tap/EMS-CE/8.5.0/TIB_ems-ce_8.5.0_linux_x86_64.zip?SJCDPTPG=1561850626_b02e19452e9b4ac2da7a035692e93be2&ext=.zip && \
    unzip TIB_ems_8.2.1_linux_x86.zip -d ems && \
    cd ems && \
    ./TIBCOUniversalInstaller-lnx-x86.bin -silent && \
    cd / && \
    rm -rf /tmp/install
