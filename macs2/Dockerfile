FROM ubuntu:20.04

RUN apt-get update

RUN apt-get install -y \
    python3 \
    python3-pip \
    python3-numpy

COPY MACS2-2.2.7.1.tar.gz /tmp
WORKDIR /tmp
RUN tar zxvf MACS2-2.2.7.1.tar.gz
WORKDIR MACS2-2.2.7.1
RUN python3 ./setup.py build
RUN python3 ./setup.py install

#test macs2
WORKDIR /tmp
RUN macs2 --help ; exit 0





    

