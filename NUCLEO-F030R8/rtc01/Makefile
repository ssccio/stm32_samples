
ARMGNU = arm-none-eabi

AOPS = --warn --fatal-warnings -mcpu=cortex-m0
COPS = -Wall -Werror -O2 -nostdlib -nostartfiles -ffreestanding  -mcpu=cortex-m0

LOPS = -Wall -m32 -emit-llvm -target arm-none-eabi -mcpu=cortex-m0 -mthumb
LLCOPS = -march=thumb -mcpu=cortex-m0
#LLCOPS = -mcpu=cortex-m0
COPS = -Wall  -O2 -nostdlib -nostartfiles -ffreestanding
OOPS = -std-compile-opts

gcc : rtc01.gcc.thumb.flash.bin 

all : gcc clang

clang : rtc01.clang.thumb.norm.flash.bin rtc01.clang.thumb.opt.flash.bin 

clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list
	rm -f *.bc
	rm -f *.opt.s
	rm -f *.norm.s

#---------------------------------

flash.o : flash.s
	$(ARMGNU)-as $(AOPS) flash.s -o flash.o

rtc01.gcc.thumb.o : rtc01.c
	$(ARMGNU)-gcc $(COPS) -mthumb -c rtc01.c -o rtc01.gcc.thumb.o

rtc01.gcc.thumb.flash.bin : flash.ld flash.o rtc01.gcc.thumb.o
	$(ARMGNU)-ld -o rtc01.gcc.thumb.flash.elf -T flash.ld flash.o rtc01.gcc.thumb.o
	$(ARMGNU)-objdump -D rtc01.gcc.thumb.flash.elf > rtc01.gcc.thumb.flash.list
	$(ARMGNU)-objcopy rtc01.gcc.thumb.flash.elf rtc01.gcc.thumb.flash.bin -O binary

#---------------------------------

rtc01.clang.bc : rtc01.c
	clang $(LOPS) -c rtc01.c -o rtc01.clang.bc

rtc01.clang.thumb.norm.flash.bin : flash.ld flash.o rtc01.clang.bc
	#llc $(LLCOPS) rtc01.clang.bc -o rtc01.clang.thumb.norm.s
	#$(ARMGNU)-as $(AOPS) rtc01.clang.thumb.norm.s -o rtc01.clang.thumb.norm.o
	llc $(LLCOPS) rtc01.clang.bc -filetype=obj -o rtc01.clang.thumb.norm.o
	$(ARMGNU)-ld -o rtc01.clang.thumb.norm.flash.elf -T flash.ld flash.o rtc01.clang.thumb.norm.o
	$(ARMGNU)-objdump -D rtc01.clang.thumb.norm.flash.elf > rtc01.clang.thumb.norm.flash.list
	$(ARMGNU)-objcopy rtc01.clang.thumb.norm.flash.elf rtc01.clang.thumb.norm.flash.bin -O binary

rtc01.clang.thumb.opt.flash.bin : flash.ld flash.o rtc01.clang.bc
	opt $(OOPS) rtc01.clang.bc -o rtc01.clang.thumb.opt.bc
	#llc $(LLCOPS) rtc01.clang.thumb.opt.bc -o rtc01.clang.thumb.opt.s
	#$(ARMGNU)-as $(AOPS) rtc01.clang.thumb.opt.s -o rtc01.clang.thumb.opt.o
	llc $(LLCOPS) rtc01.clang.thumb.opt.bc -filetype=obj -o rtc01.clang.thumb.opt.o
	$(ARMGNU)-ld -o rtc01.clang.thumb.opt.flash.elf -T flash.ld flash.o rtc01.clang.thumb.opt.o
	$(ARMGNU)-objdump -D rtc01.clang.thumb.opt.flash.elf > rtc01.clang.thumb.opt.flash.list
	$(ARMGNU)-objcopy rtc01.clang.thumb.opt.flash.elf rtc01.clang.thumb.opt.flash.bin -O binary




