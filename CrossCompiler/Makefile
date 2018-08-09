install:
	sudo apt install build-essential bison flex libgmp3-dev libmpc-dev libmpfr-dev texinfo

preparation:
	source preparation.sh

build-binutils:
	cd src/build-binutils && \
	../binutils-2.30/configure --target=$$TARGET --prefix="$$PREFIX" --with-sysroot --disable-nls --disable-werror && \
	make && make install

build-gcc:
	cd src/build-gcc && \
	../gcc-8.1.0/configure --target=$$TARGET --prefix="$$PREFIX" --disable-nls --enable-languages=c,c++ --without-headers && \
	make all-gcc && make all-target-libgcc && \
	make install-gcc && make install-target-libgcc

build: build-binutils build-gcc 
