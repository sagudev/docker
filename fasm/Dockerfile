FROM       ubuntu:16.04

ENV FASM_VERSION 1.72

RUN apk add --no-cache curl && \
    curl -sL "https://flatassembler.net/fasm-$FASM_VERSION.tgz" | tar xz && \
ln -s /fasm/fasm /bin/fasm