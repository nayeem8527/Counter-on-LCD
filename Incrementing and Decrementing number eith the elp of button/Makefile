CC=avr-gcc
CFLAGS=-Wall -Os -DF_CPU=$(F_CPU) -mmcu=$(MCU)
MCU=atmega328p
F_CPU=16000000UL

OBJCOPY=avr-objcopy
BIN_FORMAT=ihex

PORT=/dev/ttyUSB0
BAUD=115200
PROTOCOL=arduino
PART=m328p
AVRDUDE=avrdude -F -V

RM=rm -f

all: Interrupt.hex
	sudo $(AVRDUDE) -c$(PROTOCOL) -p $(PART) -P $(PORT) -b $(BAUD) -D -U flash:w:$<

compile: Interrupt.hex

Interrupt.hex: Interrupt.elf 
	 $(OBJCOPY) -O $(BIN_FORMAT) -R .eeprom $< $@

Interrupt.elf: Interrupt.o 
	 $(CC) $(CFLAGS) -o $@ $<

Interrupt.o: Interrupt.c 
	 $(CC) $(CFLAGS) -c -o $@ $<

upload : 
	sudo $(AVRDUDE) -c $(PROTOCOL) -p $(PART) -P $(PORT) $(BAUD) -U flash:w:Interrupt.hex

clean:
	$(RM) Interrupt.elf Interrupt.hex Interrupt.s Interrupt.o


