
ARMGNU = arm-none-eabi
#ARMGNU = arm-linux-gnueabi

AOPS = --warn --fatal-warnings 
 -mcpu=cortex-m3
COPS = -Wall -Werror -O2 -nostdlib -nostartfiles -ffreestanding 
 -mcpu=cortex-m0

all : blinker01.thumb.bin blinker01.thumb.dfu.bin blinker01.thumb2.bin blinker01.thumb2.dfu.bin

clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list
	rm -f *.bc
	rm -f *.opt.s
	rm -f *.norm.s
	rm -f *.hex

#---------------------------------

flash.o : flash.s
	$(ARMGNU)-as $(AOPS) flash.s -o flash.o

blinker01.thumb.o : blinker01.c
	$(ARMGNU)-gcc $(COPS) -mthumb -mcpu=cortex-m0 -march=armv6-m -c blinker01.c -o blinker01.thumb.o

blinker01.thumb2.o : blinker01.c
	$(ARMGNU)-gcc $(COPS) -mthumb -mcpu=cortex-m3 -march=armv7-m -c blinker01.c -o blinker01.thumb2.o

blinker01.thumb.bin : flash.ld flash.o blinker01.thumb.o
	$(ARMGNU)-ld -o blinker01.thumb.elf -T flash.ld flash.o blinker01.thumb.o
	$(ARMGNU)-objdump -D blinker01.thumb.elf > blinker01.thumb.list
	$(ARMGNU)-objcopy blinker01.thumb.elf blinker01.thumb.bin -O binary

blinker01.thumb2.bin : flash.ld flash.o blinker01.thumb2.o
	$(ARMGNU)-ld -o blinker01.thumb2.elf -T flash.ld flash.o blinker01.thumb2.o
	$(ARMGNU)-objdump -D blinker01.thumb2.elf > blinker01.thumb2.list
	$(ARMGNU)-objcopy blinker01.thumb2.elf blinker01.thumb2.bin -O binary


blinker01.thumb.dfu.bin : flashdfu.ld flash.o blinker01.thumb.o
	$(ARMGNU)-ld -o blinker01.thumb.dfu.elf -T flashdfu.ld flash.o blinker01.thumb.o
	$(ARMGNU)-objdump -D blinker01.thumb.dfu.elf > blinker01.thumb.dfu.list
	$(ARMGNU)-objcopy blinker01.thumb.dfu.elf blinker01.thumb.dfu.bin -O binary

blinker01.thumb2.dfu.bin : flashdfu.ld flash.o blinker01.thumb2.o
	$(ARMGNU)-ld -o blinker01.thumb2.dfu.elf -T flashdfu.ld flash.o blinker01.thumb2.o
	$(ARMGNU)-objdump -D blinker01.thumb2.dfu.elf > blinker01.thumb2.dfu.list
	$(ARMGNU)-objcopy blinker01.thumb2.dfu.elf blinker01.thumb2.dfu.bin -O binary



