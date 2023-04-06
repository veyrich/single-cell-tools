FROM ubuntu:22.04

RUN apt update
RUN apt upgrade -y
RUN apt install -y \
    wget

WORKDIR /tmp
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.1.0-1-Linux-x86_64.sh
RUN bash Miniconda3-py310_23.1.0-1-Linux-x86_64.sh -b -p /miniconda
ENV PATH=$PATH:/miniconda/bin
RUN conda init
WORKDIR /

RUN /bin/sh



