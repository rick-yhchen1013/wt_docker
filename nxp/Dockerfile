FROM ubuntu:18.04

RUN ln -snf /usr/share/zoneinfo/Asia/Taipei /etc/localtime && echo "Asia/Taipei"  > /etc/timezone

# Install packages
# libncurses5-dev and screen is used for menuconfig of linux kernel
# sudo vim tzdata apt-utils dialog locales is used for better operation experience
# other packages are required by the Yocto project and Android
RUN apt-get update && apt-get -y install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint3 xterm rsync curl sudo vim tzdata apt-utils dialog locales screen libncurses5-dev uuid uuid-dev zlib1g-dev liblz-dev liblzo2-2 liblzo2-dev lzop u-boot-tools mtd-utils android-tools-fsutils device-tree-compiler gdisk m4 libz-dev bison flex libssl-dev gcc-multilib bc zip

# Toolchain for Android compilation
COPY gcc-arm-8.3-2019.03-x86_64-aarch64-elf.tar.xz /

# To create /home/user/.profile to workaround bash variable missing after "docker start" and "docker attach"
RUN tar -xvJf gcc-arm-8.3-2019.03-x86_64-aarch64-elf.tar.xz -C /opt && rm gcc-arm-8.3-2019.03-x86_64-aarch64-elf.tar.xz && locale-gen en_US.UTF-8 && useradd -u 1000 user && mkdir -p /home/user/bin /work /opt /work2 /work3 && echo "export LC_ALL=en_US.UTF-8" >> /home/user/.profile && echo "export TERM=vt220" >> /home/user/.profile && echo "export AARCH64_GCC_CROSS_COMPILE=/opt/gcc-arm-8.3-2019.03-x86_64-aarch64-elf/bin/aarch64-elf-" >> /home/user/.profile && chown -R user.user /home/user /work && echo 'user:user' | chpasswd && echo 'user ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers 


ENV LC_ALL en_US.UTF-8
# Better display for menuconfig of linux kernel
ENV TERM vt220
ENV AARCH64_GCC_CROSS_COMPILE=/opt/gcc-arm-8.3-2019.03-x86_64-aarch64-elf/bin/aarch64-elf-
USER user
RUN curl https://storage.googleapis.com/git-repo-downloads/repo > /home/user/bin/repo && chmod a+x /home/user/bin/repo && git config --global user.name "buildbot" && git config --global user.email "buildbot@wtmec.com"

