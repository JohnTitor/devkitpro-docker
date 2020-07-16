FROM debian:stretch

MAINTAINER Yuki Okushi <huyuumi.dev@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apt-utils && \
    apt-get install -y --no-install-recommends sudo ca-certificates pkg-config curl wget bzip2 xz-utils make git bsdtar doxygen gnupg && \
    apt-get install -y gdebi-core && \
    apt-get clean

RUN wget https://github.com/devkitPro/pacman/releases/latest/download/devkitpro-pacman.amd64.deb && \
    gdebi -n devkitpro-pacman.amd64.deb && \
    rm devkitpro-pacman.amd64.deb && \
    dkp-pacman -Scc --noconfirm

RUN dkp-pacman -Syyu --noconfirm switch-dev devkitA64 && \
    dkp-pacman -S --needed --noconfirm `dkp-pacman -Slq dkp-libs | grep '^switch-'` && \
    dkp-pacman -Scc --noconfirm

ENV DEVKITPRO=/opt/devkitpro
ENV PATH=${DEVKITPRO}/devkitA64/bin:$PATH
ENV PATH=${DEVKITPRO}/tools/bin:$PATH
