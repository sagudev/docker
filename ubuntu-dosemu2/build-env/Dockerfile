FROM       sagu/ubuntu-sshd:16.04



RUN apt-get update && apt install git gcc glibc* bison flex libsdl2-2.0-0 libsdl2-dev alsa -y && apt install binutils libslang2-dev libasound2-dev linux-headers-amd64 --no-install-recommends -y

RUN git clone https://github.com/stsp/dosemu2.git

ENTRYPOINT /usr/sbin/sshd -D && apt-get update -qq && cd dosemu2