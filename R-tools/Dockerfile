FROM base:latest

#disable the dpkg interactive frontend (invoked when installing tzdata)
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y \
    lsb-release \
    gnupg \
    curl

#Linux packages for end-users
RUN apt-get install -y \
    vim \
    wget \
    emacs-nox



#
#Base R install
#
RUN apt-get install -y --no-install-recommends software-properties-common dirmngr
RUN wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc
RUN add-apt-repository -y "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
RUN apt-get install -y --no-install-recommends r-base

RUN apt-get update

#
#Seurat installation
#
#pre-reqs for Seurat and dependencies
RUN apt-get install -y \
    liblapack-dev \
    libblas-dev \
    gfortran \
    libssl-dev \
    libcurlpp-dev \
    libpng-dev \
    make \
    g++ \
    git

COPY seurat-deps /tmp/seurat-deps
RUN for pkg in `cat /tmp/seurat-deps`; do echo $pkg; apt-get install -y r-cran-$pkg; done

RUN echo "install.packages('Seurat')" | R  --no-save
RUN echo "library(Seurat)" | R --no-save


#
#Dynamo (https://github.com/aristoteleo/dynamo-release)
#
RUN apt install -y \
    python3-h5py \
    python3-numpy-groupies
RUN pip3 install gitpython
RUN pip3 install mkdocs


#
#Dynamo
#
#ToDo: version conflict - see below
#
#RUN git clone https://github.com/aristoteleo/dynamo-release.git
#WORKDIR dynamo-release
#RUN python3 setup.py build
#on Ubuntu 22.04 this errors out with
#error: networkx 3.0 is installed but networkx<3.0,>=2.1 is required by {'chinese-whispers'}RUN python3 setup.py install


#
#ArchR
#

#ArchR dependencies first
RUN apt-get install -y \
    xml2 \
    lzma-dev \
    liblzma-dev \
    libgsl-dev \
    libcurl4-openssl-dev \
    r-cran-systemfonts \
    r-cran-textshaping \
    r-cran-ragg \
    r-cran-roxygen2 \
    r-cran-rversions \
    r-cran-xml2 \
    libxml2-dev \
    r-bioc-rhtslib \
    r-bioc-rsamtools \
    r-bioc-rsamtools \
    r-bioc-rtracklayer \
    r-bioc-rtracklayer \
    r-bioc-bsgenome \
    r-bioc-tfbstools \
    r-cran-gsl \
    plplot-driver-cairo

#use devtools to install additional reqs
RUN echo 'if (!requireNamespace("devtools", quietly = TRUE)) install.packages("devtools")' | R --no-save
RUN echo 'if (!requireNamespace("BiocManager", quietly = TRUE)) install.packages("BiocManager")' | R --no-save
RUN echo 'devtools::install_github("GreenleafLab/ArchR", ref="master", repos = BiocManager::repositories())' | R --no-save

###
ENTRYPOINT /bin/bash

