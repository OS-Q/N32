CFLAGS 	= -mmcs51 --std-c99
LDFLAGS = -mmcs51 --out-fmt-ihx
NAME   	?= clock
TARGET 	?= main.ihx
SRCS    := $(wildcard *.c)
OBJS     = $(SRCS:.c=.rel)
CC       = sdcc
OBJCOPY  = sdobjcopy
PACK_HEX = packihx

all: $(TARGET) size

$(TARGET): $(OBJS)
	$(CC) $(LDFLAGS) $(OBJS) -o $@
	$(PACK_HEX) $(TARGET) > $(NAME).hex
	@$(OBJCOPY) -I ihex --output-target=binary $(TARGET) $(NAME).bin
	cp $(NAME).bin ../build/
	cp $(NAME).hex ../build/

%.rel: %.c
	$(CC) $(CFLAGS) -c $< -o $@

size:
	@echo "-----BIN size:"	>> ../build/README.txt
	@stat -L -c %s $(NAME).bin 	>> ../build/README.txt
	echo "\nfinish build and upload." >> ../build/README.txt

clean:
	rm -f *.asm *.rel *.lst *.rst *.hex *.mem *.map *.sym *.lk *.ihx

.PHONY: clean all
