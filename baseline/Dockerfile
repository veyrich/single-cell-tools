FROM ubuntu:22.04

#disable the dpkg interactive frontend (invoked when installing tzdata)
ENV DEBIAN_FRONTEND=noninteractive

#baseline packages
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y apt-utils
RUN apt-get install -y \
    lsb-release \
    gnupg \
    curl

#man-db can slow down GCP SDK updates
RUN apt-get remove -y man-db

#Linux packages for end-user
RUN apt-get install -y \
    vim \
    wget


#GCS fuse
RUN echo "deb http://packages.cloud.google.com/apt gcsfuse-$(lsb_release -c -s) main" | tee /etc/apt/sources.list.d/gcsfuse.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN apt-get update
RUN apt-get install -y gcsfuse


#Google SDK
RUN apt-get install -y apt-transport-https ca-certificates gnupg
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
RUN apt-get update
RUN apt-get install -y google-cloud-cli


#Jupyter Lab
RUN apt-get install -y python3-pip
RUN pip3 install jupyterlab; exit 0


###
ENTRYPOINT /bin/bash
