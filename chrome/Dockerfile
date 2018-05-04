FROM ubuntu
ARG UID=1000
ARG GID=1000

RUN apt-get update && apt-get install -y wget
RUN apt-get install -y gnupg dbus-x11
RUN apt-get install -y sudo
 
RUN groupadd -g $GID docker
RUN echo 'ALL ALL = (ALL:ALL) NOPASSWD: ALL' >> /etc/sudoers
RUN useradd -m -d /home/docker -u $UID -g $GID -s /bin/bash -G adm,sudo docker
RUN mkdir /var/run/dbus

RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list
RUN apt-get update
RUN apt-get install google-chrome-stable dbus-x11 packagekit-gtk3-module libcanberra-gtk-module -y

USER docker
ENV HOME /home/docker
CMD sudo dbus-daemon --system --fork && google-chrome --no-sandbox

