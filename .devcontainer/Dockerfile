FROM --platform=linux/amd64 mcr.microsoft.com/vscode/devcontainers/base:0-jammy

# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends build-essential \
  wget \
  openjdk-8-jdk \
  git \
  g++ \
  cmake \
  make

ADD https://downloads.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz /usr/local
RUN ln -s /usr/local/apache-maven-3.9.6 /usr/local/maven
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64
ENV MAVEN_HOME=/usr/local/maven
ENV PATH=$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin

RUN git clone https://github.com/apache/incubator-gluten.git incubator-gluten
RUN cd incubator-gluten && ./dev/builddeps-veloxbe.sh --enable_vcpkg=ON --build_tests=OFF  --build_benchmarks=OFF --enable_s3=OFF  \
    --enable_gcs=ON --enable_hdfs=ON --enable_abfs=ON --build_type=Debug
RUN mvn clean install -Pspark-3.5 -Pbackends-velox -Prss -Piceberg -Pdelta -DskipTests
