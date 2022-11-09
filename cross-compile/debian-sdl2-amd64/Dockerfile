
FROM tomtzook/cross-compile:debian-base-amd64


RUN apt-get install libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev libglm-dev -y

# Download and extract SDL2
ENV SDL2_VERSION 2.0.12
RUN wget -c https://github.com/libsdl-org/SDL/releases/download/release-${SDL2_VERSION}/SDL2-${SDL2_VERSION}.tar.gz -O - | tar -xz && \
	mv SDL2-${SDL2_VERSION} SDL2

# Build and install SDL2 for amd64 (host)
RUN cd SDL2 && mkdir build && cd build && \
	../configure && \
	make && make install && \
	cd .. && rm -rf build

# Build and install SDL2 for windows
RUN cd SDL2 && mkdir build && cd build && \
	PREFIX=/usr/ && \
	TOOLSET=x86_64-w64-mingw32 && \
	export CC="$TOOLSET-gcc -static-libgcc" && \
	../configure --target=$TOOLSET --host=$TOOLSET --build=x86_64-linux --prefix=$PREFIX/$TOOLSET && \
	make && make install && \
	cd .. && rm -rf build

# Build and install SDL2 for aarch64
# pulseaudio and alsa disabled due to missing libraries
RUN cd SDL2 && mkdir build && cd build && \
	PREFIX=/usr/ && \
	TOOLSET=aarch64-linux-gnu && \
	export CC="$TOOLSET-gcc -static-libgcc" && \
	../configure --target=$TOOLSET --host=$TOOLSET --build=x86_64-linux --prefix=$PREFIX/$TOOLSET --disable-alsa --disable-pulseaudio --enable-esd=no && \
	make && make install && \
	cd .. && rm -rf build

# Build and install SDL2 for arm gnueabihf
# pulseaudio and alsa disabled due to missing libraries
RUN cd SDL2 && mkdir build && cd build && \
	PREFIX=/usr/ && \
	TOOLSET=arm-linux-gnueabihf && \
	export CC="$TOOLSET-gcc -static-libgcc" && \
	../configure --target=$TOOLSET --host=$TOOLSET --build=x86_64-linux --prefix=$PREFIX/$TOOLSET --disable-alsa --disable-pulseaudio --enable-esd=no && \
	make && make install && \
	cd .. && rm -rf build