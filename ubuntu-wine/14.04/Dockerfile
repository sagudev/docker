FROM       sagu/ubuntu-sshd:14.04

RUN apt-get update && apt install sudo

RUN addgroup --system xusers \
  && adduser \
			--home /home/xclient \
			--disabled-password \
			--shell /bin/bash \
			--gecos "user for running an xclient application" \
			--ingroup xusers \
			--quiet \
			xclient

RUN usermod -a -G sudo xusers && echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Install packages required for connecting against X Server
RUN apt-get update && apt-get install -y --no-install-recommends \
				xauth \
		&& rm -rf /var/lib/apt/lists/*


USER root

# Install some tools required for creating the image
RUN apt-get install -y --no-install-recommends \
		curl \
		unzip \
		ca-certificates \
		sudo

# Install wine and related packages
RUN dpkg --add-architecture i386 \
		&& apt-get update \
		&& apt-get install -y \
				wine \
				wine32* \
		&& rm -rf /var/lib/apt/lists/*

# Wine really doesn't like to be run as root, so let's use a non-root user
USER xclient
ENV HOME /home/xclient
ENV WINEPREFIX /home/xclient/.wine
ENV WINEARCH win32

# Use xclient's home dir as working dir
WORKDIR /home/xclient

RUN echo "alias winegui='wine explorer /desktop=DockerDesktop,1024x768'" > ~/.bash_aliases 
# During startup we need to prepare connection to X11-Server container
USER xclient
ENTRYPOINT sudo apt-get update -q && /usr/sbin/sshd -D && export DISPLAY=xserver:0 && xauth merge /Xauthority/xserver.xauth && echo If you want to run app as root use sudo or login to root with password root