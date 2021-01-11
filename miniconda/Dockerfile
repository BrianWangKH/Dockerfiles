# base image
FROM ubuntu

# system setup
#RUN apt-get update && apt-get upgrade -y && \
RUN apt-get update && apt-get install -y wget

# Install miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    bash Miniconda3-latest-Linux-x86_64.sh -b -p /home/miniconda && \
    # -b -- Batch mode with no PATH modifications to .bashrc \
    # assumes you agree to the licence agreement
    # -p -- Installation prefix/path
    rm Miniconda3-latest-Linux-x86_64.sh

ENV PATH=/home/miniconda/bin:${PATH}
# add a new path into PATH list
# ${PATH} is the original list of paths

# conda setup
RUN conda update -y conda && \
    conda --version
# conda config --set auto_activate_base false