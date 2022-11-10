
FROM tomtzook/cross-compile:debian-base-amd64


# Download and extract OpenCV
ENV OPENCV_VERSION 4.6.0
RUN wget -c https://github.com/opencv/opencv/archive/refs/tags/${OPENCV_VERSION}.tar.gz -O - | tar -xz && \
	mv opencv-${OPENCV_VERSION} opencv

# Build and install for amd64 (host)
RUN cd opencv && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release && \
	make && make install && \
	cd .. && rm -rf build

# Get cmake toolchain files
RUN git clone https://github.com/tomtzook/cmake-toolchain-files.git cmake-toolchain-files

# Build and install for windows x86_64
RUN cd opencv && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=/cmake-toolchain-files/x86_64-mingw-gcc-pthread.cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/x86_64-w64-mingw32 && \
	make && make install && \
	cd .. && rm -rf build

# Build and install for aarch64
RUN cd opencv && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=/cmake-toolchain-files/aarch64-linux-gnu-gcc.cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/aarch64-linux-gnu && \
	make && make install && \
	cd .. && rm -rf build

# Build and install arm gnueabihf
RUN cd opencv && mkdir build && cd build && \
	cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=/cmake-toolchain-files/arm-linux-gnueabihf-gcc.cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/arm-linux-gnueabihf && \
	make && make install && \
	cd .. && rm -rf build
