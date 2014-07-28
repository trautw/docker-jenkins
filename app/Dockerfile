FROM     ubuntu:14.04
MAINTAINER Christoph Trautwein "christoph.trautwein@sinnerschrader.com"

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y less && \
  apt-get install -y vim

RUN echo root:`dd if=/dev/urandom count=250 2>/dev/null | sha1sum | tail -n 1 | cut -f1 -d\ ` |chpasswd

RUN apt-get install -y git-core

RUN apt-get install -y wget
RUN wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
RUN echo "deb http://pkg.jenkins-ci.org/debian binary/" >> /etc/apt/sources.list
RUN apt-get update
# RUN apt-get install -y jenkins=1.550
# RUN apt-get install -y jenkins=1.564
RUN apt-get install -y jenkins

ENV JENKINS_HOME /volume/data

ENTRYPOINT chown jenkins: $JENKINS_HOME && exec su jenkins -c "java -jar /usr/share/jenkins/jenkins.war"
EXPOSE 8080
CMD [""]
