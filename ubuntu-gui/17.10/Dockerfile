FROM       sagu/ubuntu-sshd:17.10

RUN apt install firefox -y && echo "DISPLAY=192.168.99.1:0" >> /etc/environment
ENTRYPOINT apt-get update -q && /usr/sbin/sshd -D