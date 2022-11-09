
FROM tomtzook/cross-compile:debian-base-amd64


RUN apt-get install libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev libglm-dev -y


# Build and install SDL2 for windows
RUN wget -c https://github.com/libsdl-org/SDL/releases/download/release-2.24.2/SDL2-2.24.2.tar.gz -O - | tar -xz && \
	cd SDL2-2.24.2 && \
	mkdir build && cd build && \
	PREFIX=/usr/ && \
	TOOLSET=x86_64-w64-mingw32 && \
	export CC="$TOOLSET-gcc -static-libgcc" && \
	../configure --target=$TOOLSET --host=$TOOLSET --build=x86_64-linux --prefix=$PREFIX/$TOOLSET && \
	make && make install && \
	cd .. && rm -rf build