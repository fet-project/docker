FROM ubuntu:16.04
MAINTAINER Julio Gonzalez Gil <git@juliogonzalez.es>

USER root

# Default UID/GID for mounting folders (used at jenkins slaves)
ARG UID=500
ARG GID=500

# Create fet group and user according to arguments UID/GID
RUN groupadd -g ${GID} fet
RUN useradd -d /home/fet -u ${UID} -g ${GID} -G sudo fet && \
    mkdir /home/fet && \
    chown fet:fet /home/fet

# Create the wrappers to check for updates and to keep the container running
ADD files/*.sh /opt/

# Pass the output of date command as DATE argument if you want 
# make sure that the image is generated using the lastest 
# packages (cache will be used for previous steps)
ARG DATE=None

# generate a list of original packages, upgrade and install needed packages
RUN dpkg --get-selections | grep 'install' | grep -v 'deinstall'|cut -f1 > /opt/packages-image.txt && \
    apt-get -qq -o=Dpkg::Use-Pty=0 update > /dev/null && \
    LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 DEBIAN_FRONTEND=noninteractive apt-get -qq -o=Dpkg::Use-Pty=0 -y dist-upgrade > /dev/null && \
    LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 DEBIAN_FRONTEND=noninteractive apt-get -qq -o=Dpkg::Use-Pty=0 -y install \
     cppcheck \
     git \
     g++ \
     make \
     qtbase5-dev \
     qt5-default \
     sudo && \
    apt-get -qq -o=Dpkg::Use-Pty=0 clean > /dev/null # ${DATE}

USER fet

CMD ["/bin/bash", "/opt/start_wait.sh"]
