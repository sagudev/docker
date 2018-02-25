# Ubuntu-sshd

Dockerized SSH service with x11, built on top of [official Ubuntu](https://registry.hub.docker.com/_/ubuntu/) images.

## Image tags

- sagudev/ubuntu-gui:14.04 (trusty)
- sagudev/ubuntu-gui:16.04 (xenial, latest)
- sagudev/ubuntu-gui:17.10 (artful)
- sagudev/ubuntu-gui:18.04 (bionic, dev)



## Installed packages

Image specific:
- [openssh-server](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Config:

  - `PermitRootLogin yes`
  - `UsePAM no`
  - exposed port 22
  - default command: `/usr/sbin/sshd -D`
  - root password: `root`

## Run example

```bash
$ sudo docker run -d -P --name test_sshd rastasheep/ubuntu-sshd:14.04
$ sudo docker port test_sshd 22
  0.0.0.0:49154

$ ssh root@localhost -p 49154
# The password is `root`
root@test_sshd $
```
$ firefox
and you will see firefox
if you don't make sure that you run Xming.exe :0 -multiwindow -clipboard -ac (Windows)

