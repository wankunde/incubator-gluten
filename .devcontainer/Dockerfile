# [Choice] Ubuntu version (use ubuntu-22.04 or ubuntu-18.04 on local arm64/Apple Silicon): ubuntu-22.04, ubuntu-20.04, ubuntu-18.04
ARG VARIANT=ubuntu-20.04
ARG PLATFORM=linux/amd64
FROM --platform=${PLATFORM} mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends build-essential \
  openjdk-8-jdk \
  git \
  g++ \
  cmake \
  make

ADD apache-maven-3.9.6-bin.tar.gz /usr/local
RUN ln -s /usr/local/apache-maven-3.9.6 /usr/local/maven
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64
ENV MAVEN_HOME=/usr/local/maven
ENV PATH=$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin
