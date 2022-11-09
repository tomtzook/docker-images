
FROM debian:stable-slim

RUN apt-get update -y && \
    apt-get autoremove -y


# Install build tools
RUN apt-get install git make cmake wget gcc g++ -y && \
	apt-get install mingw-w64 mingw-w64-tools -y && \
	apt-get install gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf gcc-arm-linux-gnueabi g++-arm-linux-gnueabi gcc-aarch64-linux-gnu g++-aarch64-linux-gnu -y

# Install and configure Java
RUN apt-get install openjdk-11-jdk -y
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64
RUN export JAVA_HOME
