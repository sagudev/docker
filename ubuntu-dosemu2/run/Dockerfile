FROM       sagu/ubuntu-dosemu2:build-env

RUN cd dosemu2 && ./autogen.sh && ./default-configure && make && make install
ENTRYPOINT /usr/sbin/sshd -D && apt-get update -qq && cd dosemu2