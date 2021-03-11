CFLAGS = -mmcs51 --std-c99
NAME   ?= clock

%.hex : %.ihx
	packihx $< > $@

%.ihx : %.c stc15_buttons.rel stc15_dusk.rel stc15_display.rel ds1302.rel
	sdcc ${CFLAGS} $^

%.rel : %.c %.h
	sdcc ${CFLAGS} -c $<

.PHONY: all
all: $(NAME).hex size
	cp $(NAME).hex ../build

size:
	@echo "-----\nImage size:"
	@stat -L -c %s $(NAME).bin

.PHONY: clean
clean:
	$(RM) *.asm *.rel *.lst *.rst *.hex *.mem *.map *.sym *.lk *.ihx
