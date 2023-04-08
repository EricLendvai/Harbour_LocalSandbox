#To take advantage of Docker caching, we are using the same instructions as other .devcontainer/Dockerfile until the "RUN ldconfig"
FROM ubuntu:22.04

## for apt to be noninteractive
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

# Used by running apps to detect if inside a docker container. Testing for existence of /.dockerenv may not always work.
ENV InDocker=True

RUN apt-get update && apt-get install -y apt-utils

# Run update again to work around git install failure introduced around April 2023
RUN apt-get update

RUN apt-get install -y \
        libfcgi-dev \
        libapache2-mod-fcgid \
        git \
        build-essential \
        unixodbc-dev \
        apache2 \
        libapache2-mod-fcgid \
        libgpm2 \
        gnupg \
        wget \
        psmisc \
        libcurl4-openssl-dev

# install harbour from src
RUN mkdir /src
WORKDIR /src
RUN git clone --branch master https://github.com/harbour/core.git harbour
WORKDIR /src/harbour
ENV HB_WITH_CURL=/usr/include/x86_64-linux-gnu/
# Will request the make app to use up to 8 core.
RUN make -j 8 install

#To fix symlinks
RUN ldconfig

# Stopped using the git clone during development. Instead install the 3 repos in a location wwhere the mounts commands in devcontainer.json will make them available for this project.
# # clone and make libs
# RUN mkdir /src
# WORKDIR /src
# RUN git clone https://github.com/EricLendvai/Harbour_FastCGI/
# RUN git clone https://github.com/EricLendvai/Harbour_VFP/
# RUN git clone https://github.com/EricLendvai/Harbour_ORM/

# ENV BuildMode release
# ENV HB_COMPILER gcc
# ENV HB_VFP_ROOT /src/Harbour_VFP/
# ENV HB_ORM_ROOT /src/Harbour_ORM/
# ENV HB_FASTCGI_ROOT /src/Harbour_FastCGI/

# WORKDIR /src/Harbour_VFP
# RUN chmod +x ./BuildLIB.sh
# ENV LIBName hb_vfp
# RUN ./BuildLIB.sh

# WORKDIR /src/Harbour_ORM
# RUN chmod +x ./BuildLIB.sh
# ENV LIBName hb_orm
# RUN ./BuildLIB.sh

# #also build debug libraries
# ENV BuildMode debug

# WORKDIR /src/Harbour_VFP
# RUN chmod +x ./BuildLIB.sh
# ENV LIBName hb_vfp
# RUN ./BuildLIB.sh

# WORKDIR /src/Harbour_ORM
# RUN chmod +x ./BuildLIB.sh
# ENV LIBName hb_orm
# RUN ./BuildLIB.sh

#Required for the a2enmod
USER root

RUN a2enmod rewrite
RUN mkdir -p /var/www/Harbour_websites/fcgi_Harbour_LocalSandbox/apache-logs/

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

#Fake command to force not using a cache from this point on.
ARG CACHEBUST=3

COPY ./FilesForPublishedWebsites/LinuxApache2/Harbour_LocalSandbox.conf /etc/apache2/sites-enabled/000-default.conf
COPY ./FilesForPublishedWebsites/LinuxApache2/fcgid.conf /etc/apache2/mods-available/

COPY ./FilesForPublishedWebsites/backend/config_linux.txt /var/www/Harbour_websites/fcgi_Harbour_LocalSandbox/backend/config.txt
#RUN cp /src/build/lin64/gcc/release/FCGIHarbour_LocalSandbox.exe /var/www/Harbour_websites/fcgi_Harbour_LocalSandbox/backend/
COPY ./FilesForPublishedWebsites/website /var/www/Harbour_websites/fcgi_Harbour_LocalSandbox/website

RUN chown -R www-data:www-data /var/www/Harbour_websites

RUN update-rc.d apache2  defaults
#RUN update-rc.d postgresql  defaults

RUN mkdir -p /opt/Harbour_LocalSandbox_Data
RUN chmod -R a+rwx /opt/Harbour_LocalSandbox_Data/
