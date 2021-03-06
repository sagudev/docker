## Mozilla build environment in docker

### What's included

- all dependencies for building firefox
- MozPhab
- hg is configured (except with your username)
- you can even run firefox from docker

### Some instructions

To access bash (change '/home/user/mozilla-central' to your mozilla-central folder):

```sh
docker run -it --rm --volume="$HOME/.Xauthority:/root/.Xauthority:rw" --env="DISPLAY" --net=host -v /home/$USER/mozilla-central:/mozilla sagu/mozilla
```

or if you do not plan to use GUI:

```sh
docker run -it --rm -v /home/$USER/mozilla-central:/mozilla sagu/mozilla
```

To store data of phab and setups use:
```sh
docker run -it --rm --volume="$HOME/.Xauthority:/root/.Xauthority:rw" --env="DISPLAY" --net=host -v /home/$USER/mozilla-central:/mozilla -v /home/$USER/data:/home/wizard sagu/mozilla
```
first mach bootstrap could take long.

#### First time
If you do not have mozilla-central folder yet, you make an empty directory:
```sh
mkdir -p /home/$USER/mozilla-central
```
and then run above Docker command. When you get to shell type:
```sh
hg clone https://hg.mozilla.org/mozilla-central/ .
```
and then you are ready to help firefox.

#### Every time run when you enter container run:
```sh
./mach bootstrap
```

#### Set up username in repo
```sh
nano ./hg/hgrc
```