
FROM tomtzook/cross-compile:debian-base-amd64

# install depdendencies 
RUN apt-get install autoconf libtool -y

# Download and extract libmodbus
ENV LIBMODBUS_VERSION 3.1.10
RUN wget -c https://github.com/stephane/libmodbus/archive/refs/tags/v${LIBMODBUS_VERSION}.tar.gz -O - | tar -xz && \
	mv libmodbus-${LIBMODBUS_VERSION} libmodbus

# prepare libmodbus
RUN cd libmodbus && ./autogen.sh && cd ..

# Build and install for amd64 (host)
RUN cd libmodbus && ./configure && make install && make clean && cd ..

# Build and install for aarch64
RUN cd libmodbus && ./configure --host=aarch64-linux-gnu --prefix=/usr/aarch64-linux-gnu && \
 	make install && make clean && cd ..

# Build and install arm gnueabihf
RUN cd libmodbus && ./configure --host=arm-linux-gnueabihf --prefix=/usr/arm-linux-gnueabihf && \ 
	make install && make clean && cd ..
