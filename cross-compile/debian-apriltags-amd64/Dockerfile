
FROM tomtzook/cross-compile:debian-base-amd64


# Download and extract AprilTags
ENV APRILTAGS_VERSION 3.2.0
RUN wget -c https://github.com/AprilRobotics/apriltag/archive/refs/tags/v${APRILTAGS_VERSION}.tar.gz -O - | tar -xz && \
	mv apriltag-${APRILTAGS_VERSION} apriltag

# Get cmake toolchain files
RUN git clone https://github.com/tomtzook/cmake-toolchain-files.git cmake-toolchain-files

# Build and install for amd64 (host)
RUN cd apriltag && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release && \
	make && make install && \
	cd .. && rm -rf build

# Build and install for windows x86_64
RUN cd apriltag && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=/cmake-toolchain-files/x86_64-mingw-gcc.cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/x86_64-w64-mingw32 && \
	make && make install && \
	cd .. && rm -rf build

# Build and install for aarch64
RUN cd apriltag && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=/cmake-toolchain-files/aarch64-linux-gnu-gcc.cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/aarch64-linux-gnu && \
	make && make install && \
	cd .. && rm -rf build

# Build and install arm gnueabihf
RUN cd apriltag && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=/cmake-toolchain-files/arm-linux-gnueabihf-gcc.cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/arm-linux-gnueabihf && \
	make && make install && \
	cd .. && rm -rf build