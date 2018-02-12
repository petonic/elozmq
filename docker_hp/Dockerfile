#
# Dockerfile to build a Docker image for the ELS-HP server
# running Ubuntu
#

FROM ubuntu
MAINTAINER Mike Petonic <petonic@yahoo.com>

# Update install catalog
RUN apt-get update

# Install wget, joe, less
RUN apt-get -y install wget joe less \
    libtool pkg-config build-essential autoconf  automake

#
# Misc utilities
#
RUN apt-get install -y net-tools iputils-ping


# --- Commenting out, but working, but trying newest version
## Download zeromq
## Ref http://zeromq.org/intro:get-the-software
#RUN wget http://download.zeromq.org/zeromq-4.1.3.tar.gz
#


# Install LibSodium -- verion 18 is current on Ubuntu
RUN apt-get install -y libsodium-dev

# Install OpenPGM
RUN apt-get install -y libpgm-5.2-0 libpgm-dev

RUN cd /tmp && git clone --depth 1 --branch v4.2.3 git://github.com/zeromq/libzmq.git && cd libzmq && ./autogen.sh && ./configure --with-pgm && make && make install

## Unpack tarball package
#RUN tar xvzf zeromq-4.1.3.tar.gz

# Install dependency
RUN apt-get install -y libtool pkg-config build-essential autoconf automake uuid-dev

## Install zmq
#RUN cd zeromq-4.1.3 && \
#    sed -iBAK 's/-Werror//g' configure && \
#    ./configure --with-pgm && \
#    make install && ldconfig


# Expected
############################################################
# libzmq.so.5 (libc6,x86-64) => /usr/local/lib/libzmq.so.5
# libzmq.so (libc6,x86-64) => /usr/local/lib/libzmq.so
############################################################

RUN apt-get install -y python3 python-pip-whl python3-pip python3-dev

# Install Pyzmq
RUN python3 -m pip install --no-use-wheel pyzmq --install-option="--zmq=/usr/local/"
