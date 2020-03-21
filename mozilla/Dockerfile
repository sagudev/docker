FROM ubuntu:18.04

RUN apt update && apt upgrade -y && apt install wget curl firefox python-pip -y

RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain stable -y

ENV PATH=~/.cargo/bin:$PATH
RUN pip install mercurial hg-evolve
RUN wget -q https://hg.mozilla.org/mozilla-central/raw-file/default/python/mozboot/bin/bootstrap.py -O bootstrap.py && python bootstrap.py --application-choice=browser --no-interactive; exit 0
RUN apt-get clean
RUN hg clone https://hg.mozilla.org/hgcustom/version-control-tools /root/.mozbuild/version-control-tools
COPY .hgrc /root

ENV SHELL /bin/bash
ENV CCACHE_DIR /ccache
RUN mkdir /mozilla /ccache
WORKDIR /mozilla
