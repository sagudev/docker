FROM       sagu/ubuntu-sshd:16.04

ENV FASM_VERSION 1.72

RUN apt update && apt install curl --no-install-recommends -y && \
    curl -sL "https://flatassembler.net/fasm-$FASM_VERSION.tgz" | tar xz && \
ln -s /fasm/fasm /bin/fasm