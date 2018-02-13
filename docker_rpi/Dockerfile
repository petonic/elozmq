#
# Dockerfile to build a Docker image for the RPI clients
# running Debian
#

FROM resin/rpi-raspbian
MAINTAINER Mike Petonic <petonic@yahoo.com>

# Update install catalog
RUN apt-get update

# Install wget, joe, less
RUN apt-get update && \
    apt-get -y install \
    wget less \
    joe \
    libtool \
    pkg-config \
    build-essential \
    autoconf  \
    automake \
    uuid-dev \
    net-tools \
    iputils-ping && \
rm -rf /var/lib/apt/lists/*


# Install LibSodium -- verion 18 is current on Ubuntu
RUN apt-get update && \
    apt-get install -y \
    libsodium-dev \
    libpgm-5.2-0 \
    libpgm-dev \
&& rm -rf /var/lib/apt/lists/*

#
# Build libzmq from the static tree located in this docker build context
#
COPY libzmq_v4.2.3 /tmp/libzmq
RUN cd /tmp/libzmq && \
    ./autogen.sh && \
    ./configure --with-pgm && \
    make && \
    make install \
&& rm -rf /tmp/libzmq


RUN apt-get update && \
    apt-get install -y \
    python3 \
    python-pip-whl \
    python3-pip \
    python3-dev \
&& rm -rf /var/lib/apt/lists/*

# Install Pyzmq
# --no-use-wheel instructs pip to recompile the library instead of using
#   distribution binaries.
# --zmq=/usr/local/ instructs pip to link to the newly built libzmq
#   in /usr/local/lib, which contains the PGM protocol
RUN python3 -m pip install --no-use-wheel pyzmq --install-option="--zmq=/usr/local/"
