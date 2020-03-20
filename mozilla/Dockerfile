FROM ubuntu:18.04

RUN apt update && apt upgrade -y && apt install wget curl firefox python-pip python-setuptools -y --no-install-recommends

RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain stable -y

ENV PATH=~/.cargo/bin:$PATH
RUN pip install mercurial
RUN wget -q https://hg.mozilla.org/mozilla-central/raw-file/default/python/mozboot/bin/bootstrap.py -O bootstrap.py && python bootstrap.py --application-choice=browser --no-interactive; exit 0
RUN apt-get clean

ENV SHELL /bin/bash
ENV CCACHE_DIR /ccache
RUN mkdir /mozilla /ccache
WORKDIR /mozilla
