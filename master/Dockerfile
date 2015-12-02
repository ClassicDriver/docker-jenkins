##########################################################################################
# ClassicDriver Docker Jenkins Image
##########################################################################################
FROM jenkins:1.609.2

MAINTAINER Team Nitrous <nitrous@classicdriver.com>

#############################################
# Jenkins installation
#############################################
# Switching user to 'root' in order to create the logs folders
USER root

# Creating Log directory
RUN mkdir /var/log/jenkins

# Creating the webroot directory (where the jenkins war file willl be stored)
RUN mkdir /var/cache/jenkins

# Changing the "owner" of the operational directories back to 'jenkins'
RUN chown -R jenkins:jenkins /var/log/jenkins
RUN chown -R jenkins:jenkins /var/cache/jenkins

# Define the version of Maven
ENV MAVEN_VERSION 3.3.3

# Downloads and extract Maven from the Apache archive into /usr/share/
# Renames the extracted folder to /usr/share/maven
# Creates a simbolic link for the mvn cli in into /usr/bin
RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven

# Switching user back to 'jenkins'
USER jenkins

# Initialize Git
RUN git config --global user.name "jenkins" \
  && git config --global user.email "jenkins@classicdriver.com"

# Defaulting ENVIRONMENT variables
ENV JAVA_OPTS="-Xmx8192m"

# Sets various jenkins startup options
ENV JENKINS_OPTS="--handlerCountStartup=100 --handlerCountMax=300 --logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins/war"
