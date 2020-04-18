FROM ubuntu:18.04 AS builder
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    openssl \
    libssl1.1
RUN apt-get install -y --no-install-recommends \
    automake \
    autoconf \
    build-essential \
    libtool \
    libssl-dev \
    pkg-config \
    python-dev
    
ENV WATCHMAN_VERSION=4.9.0 \
    WATCHMAN_SHA256=1f6402dc70b1d056fffc3748f2fdcecff730d8843bb6936de395b3443ce05322
RUN cd /tmp \
 && curl --silent --location --output watchman.tar.gz "https://github.com/facebook/watchman/archive/v${WATCHMAN_VERSION}.tar.gz" \
 && echo "$WATCHMAN_SHA256 *watchman.tar.gz" | sha256sum -c - \
 && tar -xz -f watchman.tar.gz -C /tmp/ \
 && rm -rf watchman.tar.gz

RUN cd /tmp/watchman-${WATCHMAN_VERSION} \
 && ./autogen.sh \
 && ./configure --enable-lenient \
 && make \
 && make install \
 && cd $HOME \
 && rm -rf /tmp/*

FROM ubuntu:18.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt upgrade -y && apt install sudo apt-utils tzdata -y
RUN groupadd -g 1000 wizard && useradd -u 1000 -m -g 1000 wizard && usermod -g 0 wizard && echo "wizard ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER wizard
COPY --from=builder /usr/local/bin/watchman* /usr/local/bin/
COPY --from=builder /usr/local/share/doc/watchman-4.9.0 /usr/local/share/doc/watchman-4.9.0
COPY --from=builder /usr/local/var/run/watchman /usr/local/var/run/watchman
RUN sudo apt install wget curl firefox php php-curl git python3-pip python-pip libssl1.1 -y
# Rust install
RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain stable -y
ENV PATH=~/.cargo/bin:$PATH
RUN sudo pip install mercurial hg-evolve
RUN sudo pip3 install MozPhab
ENV PATH=~/.local/bin:$PATH
RUN wget -q https://hg.mozilla.org/mozilla-central/raw-file/default/python/mozboot/bin/bootstrap.py -O /home/wizard/bootstrap.py && python /home/wizard/bootstrap.py --application-choice=browser --no-interactive; exit 0
RUN sudo apt-get clean && sudo chmod 777 /usr/local/var/run/watchman
RUN hg clone https://hg.mozilla.org/hgcustom/version-control-tools /home/wizard/.mozbuild/version-control-tools
COPY .hgrc /home/wizard

ENV SHELL /bin/bash
RUN sudo mkdir /mozilla && sudo chown -R wizard /mozilla
WORKDIR /mozilla