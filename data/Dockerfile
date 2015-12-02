##########################################################################################
# ClassicDriver Docker Data Volume Image for Jenkins
##########################################################################################
FROM classicdriver/base

MAINTAINER Team Nitrous <nitrous@classicdriver.com>

#############################################
# Jenkins Data Volume setup
#############################################

# Creating the 'jenkins' user to match the user running jenkins in the application container
RUN useradd -d "/var/jenkins_home" -u 1000 -m -s /bin/bash jenkins

# Creating Log folder
RUN mkdir /var/log/jenkins

# Setting the "owner" of the logs folder back to 'jenkins'
RUN chown -R  jenkins:jenkins /var/log/jenkins

# Mounting the volume
VOLUME ["/var/log/jenkins", "/var/jenkins_home"]

# Switching user to 'jenkins' (since this is a data valume and will be used by the jenkins application container user)
USER jenkins

# Command runned once at startup
CMD ["echo", "Data container for Jenkins"]
