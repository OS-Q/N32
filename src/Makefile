CFLAGS 	= -mmcs51 --std-c99
NAME   	?= clock
TARGET 	?= main.ihx
OBJS 	= $(SRCS:.c=.rel)
OBJCOPY  = sdobjcopy
LDFLAGS  = -m$(ARCH) -l$(ARCH) --out-fmt-ihx

all: $(TARGET) size

$(TARGET): $(OBJS)
	sdcc $(LDFLAGS) $(OBJS) -o $@
	packihx $(TARGET) > $(NAME).hex
	@$(OBJCOPY) -I ihex --output-target=binary $(TARGET) $(NAME).bin
	cp $(NAME).bin ../build/
	cp $(NAME).hex ../build/

%.rel : %.c %.h
	sdcc ${CFLAGS} -c $<

size:
	@echo "-----\nImage size:"
	@stat -L -c %s $(NAME).bin
	echo "\nfinish build and upload." >> ../build/README

.PHONY: clean
clean:
	$(RM) *.asm *.rel *.lst *.rst *.hex *.mem *.map *.sym *.lk *.ihx
