FROM ubuntu:18.04

# Run the following commands as super user (root):
USER root
RUN apt-get update
RUN apt-get install -y wget tar git python python-pip dpkg-dev cmake g++ gcc \
    binutils libx11-dev libxpm-dev libxft-dev libxext-dev libtbb-dev
RUN pip install --upgrade pip

# Create a user that does not have root privileges
ARG username=physicist
RUN useradd --create-home --home-dir /home/${username} ${username}
ENV HOME /home/${username}
WORKDIR /home/${username}

# Switch to our newly created user
USER ${username}

# Instead of sh use bash:
SHELL ["/bin/bash", "-c"]

# Install ROOT binaries
ARG roottargz=root_v6.18.04.Linux-ubuntu18-x86_64-gcc7.4.tar.gz
RUN wget https://root.cern.ch/download/${roottargz}
RUN tar -zxf ${roottargz} && mv root root-6.18.04
RUN rm ${roottargz}
RUN echo "source ~/root-6.18.04/bin/thisroot.sh" >> ~/.bashrc

CMD ["bash"]
