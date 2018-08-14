AS=$$HOME/opt/cross/bin/i686-elf-as
CC=$$HOME/opt/cross/bin/i686-elf-gcc
CFLAGS= -std=gnu99 -ffreestanding -O2 -Wall -Wextra
LFLAGS= -ffreestanding -O2 -nostdlib

ODIR=obj
SDIR=src
BDIR=bin
CDIR=config

_OBJ = boot.o kernel.o
OBJ = $(patsubst %,$(ODIR)/%,$(_OBJ))

$(ODIR)/boot.o: $(SDIR)/boot.s
	@$(AS) $< -o $@

$(ODIR)/kernel.o: $(SDIR)/kernel.c
	@$(CC) -c $< -o $@ $(CFLAGS)

object: $(OBJ)

create:
	@mkdir -p isodir/boot/grub && \
	cp $(BDIR)/myos.bin isodir/boot/myos.bin && \
	cp $(CDIR)/grub.cfg isodir/boot/grub/grub.cfg && \
	grub-mkrescue -o myos.iso isodir

all: object create
	@$(CC) -T $(SDIR)/linker.ld -o $(BDIR)/myos.bin $(LFLAGS) $(OBJ) -lgcc

check:
	@if grub-file --is-x86-multiboot $(BDIR)/myos.bin; then \
		echo multiboot confirmed; \
	else \
		echo the file is not multiboot; \
	fi

.PHONY: clean

clean:
	rm -f $(ODIR)/*.o $(BDIR)/*.bin myos.iso