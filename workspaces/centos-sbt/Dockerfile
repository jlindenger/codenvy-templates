FROM codenvy/centos_jdk8

RUN curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo && \
  sudo yum install sbt -y
