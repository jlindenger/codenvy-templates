# This Dockerfile is based on the official Codenvy Node one from:
#   https://github.com/codenvy/dockerfiles/blob/master/node/latest/Dockerfile
#
# Differences:
#   - Installs latest node using the apt-get package instead of compiling it
#   - Exposes more ports (for angular2 and ionic CLI/quickstart servers
#   - Installs angular-cli and ionic

FROM codenvy/debian_jre
ENV NODE_VERSION=6.6.0 \
    NODE_PATH=/usr/local/lib/node_modules 
    
RUN sudo apt-get update && \
    sudo apt-get -y install build-essential libssl-dev libkrb5-dev gcc make ruby-full rubygems debian-keyring && \
    sudo gem install sass compass && \
    sudo apt-get clean && \
    sudo apt-get -y autoremove && \
    sudo apt-get -y clean && \
    sudo rm -rf /var/lib/apt/lists/* 

RUN set -ex \
  && for key in \
    9554F04D7259F04124DE6B476D5A82AC7E37093B \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
  ; do \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
  done 

RUN cd /home/user && curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \
  && curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
  && gpg --verify SHASUMS256.txt.asc \
  && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
  && grep " node-v$NODE_VERSION-linux-x64.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
  && sudo tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 \
  && sudo rm "node-v$NODE_VERSION-linux-x64.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt \
  && sudo ln -s /usr/local/bin/node /usr/local/bin/nodejs

# Ports
#   - Codenvy NodeJS image: 3000 5000 9000
#   - Angular2 quickstart: 3000 3001
#   - angular-cli: 4200 49152
#   - ionic2: 8100 35729 (I think)
EXPOSE 3000 3001 4200 5000 8100 9000 35729 49152

RUN sudo npm install -g npm@latest
RUN sudo npm install -g angular-cli ionic cordova

WORKDIR /projects

CMD tail -f /dev/null
