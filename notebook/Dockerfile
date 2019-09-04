FROM colomoto/colomoto-docker:2019-07-17
MAINTAINER Vincent Noel <contact@vincent-noel.fr>

USER root
WORKDIR /notebook

RUN apt-get -qq update \
    && apt-get install -y python3 python3-pip \
                          curl software-properties-common nano git apt-transport-https 

# Updating pip
RUN pip install pip --upgrade \
    && pip install setuptools --upgrade \
    && easy_install -U distribute


# Installing MaBoSS from github repo
RUN apt-get install -y flex bison \
    && git clone https://github.com/maboss-bkmc/MaBoSS-env-2.0 /usr/share/MaBoSS-env-2.0 \
    && cd /usr/share/MaBoSS-env-2.0/engine/src/ \
    && make install \
    && make MAXNODES=128 install \
    && make MAXNODES=256 install \
    && rm /opt/conda/bin/MaBoSS* \
    && ln -s /usr/share/MaBoSS-env-2.0/engine/pub/MaBoSS /opt/conda/bin \
    && ln -s /usr/share/MaBoSS-env-2.0/engine/pub/MaBoSS_128n /opt/conda/bin \
    && ln -s /usr/share/MaBoSS-env-2.0/engine/pub/MaBoSS_256n /opt/conda/bin


RUN pip install git+https://github.com/vincent-noel/pyMaBoSS.git@feat/ensemble_models  --upgrade
USER user
# Exposing port 8888 for notebook access
EXPOSE 8888




