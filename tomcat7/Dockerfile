FROM ubuntu:14.04.1
MAINTAINER Stephan Zednik "zednis2@rpi.edu"
ENV REFRESHED_AT 2015-01-27

# Install build dependencies
RUN \
  apt-get -q update && \
  apt-get -y install software-properties-common

# Install Oracle Java7 JDK
RUN \
  echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  apt-add-repository -y ppa:webupd8team/java && \
  apt-get -q update && \
  apt-get install -y oracle-java7-installer && \
  rm -rf /var/cache/oracle-jdk7-installer

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
RUN echo "JAVA_HOME=/usr/lib/jvm/java-7-oracle" >> /etc/environment

# Install Tomcat7
RUN \
  apt-get install -y -q tomcat7 && \
  apt-get clean

ENV CATALINA_BASE /var/lib/tomcat7
ENV CATALINA_HOME /usr/share/tomcat7
ENV PATH $PATH:$CATALINA_HOME/bin
RUN echo "JAVA_HOME=/usr/lib/jvm/java-7-oracle" >> /etc/default/tomcat7

# Clean up APT when done.
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME ["/var/lib/tomcat7/webapps", "/var/lib/tomcat7/conf"]

EXPOSE 8080

USER tomcat7
ENTRYPOINT ["/usr/share/tomcat7/bin/catalina.sh", "run"]