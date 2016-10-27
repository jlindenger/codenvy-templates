# This Dockerfile is based on the official Codenvy Node one from:
#   https://github.com/codenvy/dockerfiles/blob/master/node/latest/Dockerfile
#
# Differences:
#   - Installs latest node using the apt-get package instead of compiling it
#   - Exposes more ports (for angular2 and ionic CLI/quickstart servers
#   - Installs angular-cli and ionic

FROM codenvy/ubuntu_jre

ENV NODE_PATH=/usr/local/lib/node_modules 

RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - && \
    sudo apt-get update && \
    sudo apt-get -y install nodejs build-essential libssl-dev libkrb5-dev gcc make ruby-full rubygems-integration python && \
    sudo gem install sass compass && \
    sudo apt-get clean && \
    sudo apt-get -y autoremove && \
    sudo apt-get -y clean && \
    sudo rm -rf /var/lib/apt/lists/*

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
