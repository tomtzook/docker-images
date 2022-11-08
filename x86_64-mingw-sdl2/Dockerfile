
FROM debian:stable-slim

RUN apt-get update -y && \
    apt-get autoremove -y


# Install build tools
RUN apt-get install git make cmake wget gcc g++ -y && \
	apt-get install mingw-w64 mingw-w64-tools -y && \
	apt-get install libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev libglm-dev -y

# Install and configure Java
RUN apt-get install openjdk-11-jdk -y
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64
RUN export JAVA_HOME
	

# Build and install SDL2 for windows
RUN wget -c https://github.com/libsdl-org/SDL/releases/download/release-2.24.2/SDL2-2.24.2.tar.gz -O - | tar -xz && \
	cd SDL2-2.24.2 && \
	mkdir build && cd build && \
	PREFIX=/usr/ && \
	TOOLSET=x86_64-w64-mingw32 && \
	export CC="$TOOLSET-gcc -static-libgcc" && \
	../configure --target=$TOOLSET --host=$TOOLSET --build=x86_64-linux --prefix=$PREFIX/$TOOLSET && \
	make && make install
