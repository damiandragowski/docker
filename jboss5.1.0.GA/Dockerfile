FROM ubuntu
MAINTAINER Damian Dragowski <damian.dragowski@gmail.com>
RUN apt-get update && apt-get install -y wget unzip
RUN \
  echo oracle-java6-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java6-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk6-installer
EXPOSE 8080
ENV JAVA_HOME /usr/lib/jvm/java-6-oracle
ENV JBOSS_VERSION 5.1.0.GA
ENV JBOSS_HOME /opt/jboss
ENV APP_HOME /opt/jboss/server/default/deploy
ENV APP_TRANS_TIMEOUT 900
ENV APP_DIST dist

RUN cd $HOME && \
    apt-get update && apt-get install -y unzip && \
    wget -q http://sourceforge.net/projects/jboss/files/JBoss/JBoss-$JBOSS_VERSION/jboss-$JBOSS_VERSION.zip/download -O jboss-$JBOSS_VERSION.zip && \
    unzip -qo jboss-$JBOSS_VERSION.zip && \
    mkdir -p /opt/ && \
    mv $HOME/jboss-$JBOSS_VERSION $JBOSS_HOME && \
    rm -rf jboss-$JBOSS_VERSION.zip $JBOSS_HOME/server/all $JBOSS_HOME/server/minimal $JBOSS_HOME/docs
VOLUME ["$JBOSS_HOME/server/default/log"]
COPY $APP_DIST/*.* $APP_HOME/
CMD ["/opt/jboss/bin/run.sh", "-b", "0.0.0.0"]
