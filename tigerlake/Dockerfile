ROM ubuntu:20.04

RUN apt-get update
ENV TERM vt100
ENV TZ Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get -y install sudo vim tzdata apt-utils dialog python3 cpio python2.7 python2 locales python3-distutils python-distutils-extra xterm tmux
#xterm and tmux are options for linux menuconfig, but xterm need to have DISPLAY set and xorg installed
RUN update-alternatives --install /usr/bin/python python /usr/bin/python2 1
RUN apt-get -y install socat gawk wget git-core diffstat unzip texinfo build-essential chrpath libncurses5-dev patchutils curl git-lfs

RUN locale-gen en_US.UTF-8
RUN useradd -u 1000 user
RUN mkdir /home/user
RUN chown user.user /home/user
RUN echo 'user:user' | chpasswd
RUN echo 'user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER user
ENV LC_ALL en_US.UTF-8
RUN mkdir -p /home/user/bin
RUN curl https://storage.googleapis.com/git-repo-downloads/repo > /home/user/bin/repo
RUN chmod a+x /home/user/bin/repo


