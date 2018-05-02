FROM ubuntu
ARG UID=1000
ARG GID=1000
RUN mkdir -p /home/chrome && \
    echo "chrome:x:$UID:$GID:Chrome Sandbox:/home/chrome:/bin/bash" >> /etc/passwd && \
    echo "developer:x:$GID:" >> /etc/group && \
    chown $UID:$GID -R /home/chrome

RUN apt-get update && apt-get install -y wget
RUN apt-get install -y gnupg dbus-x11
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list
RUN apt-get update
RUN apt-get install google-chrome-stable dbus-x11 packagekit-gtk3-module libcanberra-gtk-module -y

USER chrome
ENV HOME /home/chrome
CMD dbus-daemon --system --fork && google-chrome

