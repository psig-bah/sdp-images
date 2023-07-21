# Copyright © 2023 Booz Allen Hamilton. All Rights Reserved.
# This software package is licensed under the Booz Allen Public License. The license can be found in the License file or at http://boozallen.github.io/licenses/bapl

FROM ghcr.io/boozallen/sdp-images/nvm:1.0.0

SHELL ["/bin/bash", "-c"]
ARG FIREFOX_VERSION=115.0.2

# install wget and bzip2
RUN dnf update -y --nodocs && \
  dnf install -y --nodocs wget bzip2

# install firefox
RUN wget https://download-installer.cdn.mozilla.net/pub/firefox/releases/${FIREFOX_VERSION}/linux-x86_64/en-US/firefox-${FIREFOX_VERSION}.tar.bz2 && \
  tar xvjf firefox-${FIREFOX_VERSION}.tar.bz2 -C /usr/local && \
  rm firefox-${FIREFOX_VERSION}.tar.bz2 && \
  ln -fs /usr/local/firefox/firefox /usr/bin/firefox

# add appstream repo and install cypress dependencies (https://docs.cypress.io/guides/continuous-integration/introduction#Dependencies)
COPY centos.repo /etc/yum.repos.d/
RUN dnf install -y xorg-x11-server-Xvfb gtk2-devel gtk3-devel libnotify-devel GConf2 nss libXScrnSaver alsa-lib

# cleanup
RUN dnf clean all && \
  rm -rf /var/cache/*

CMD ["/bin/bash"]
