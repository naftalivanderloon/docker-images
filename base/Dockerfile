# Base
#
# VERSION               0.0.1

FROM ubuntu
MAINTAINER H. Wüthrich "hw@5px.ch"

# Tell dpkg not to ask any questions
ENV DEBIAN_FRONTEND noninteractive

# This forces dpkg not to call sync() after package extraction and speeds up install
RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup

# We don't need and apt cache in a container
RUN echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache

# Make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe restricted multiverse" > /etc/apt/sources.list
RUN apt-get update && apt-get -y install eatmydata && eatmydata -- bash -c 'apt-get upgrade && apt-get -y install curl wget git-core vim htop supervisor net-tools inetutils-ping' # 10/14/2013

# Configure supervisor
ADD supervisord.conf /etc/supervisor/supervisord.conf

# Add startup script
ADD start /start

# Run supervisord
CMD ["/start/supervisord"]
