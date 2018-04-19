#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#
# Platform Overrides:
#      <Put a description of the supported Overrides here
#
#------------------------------------------------------------------------------
include sources.mk

# Platform Overrides
PLATFORM = HOST
TARGET = c1m2
LDFLAGS = -Wl,-Map=$(TARGET).map $(LINKER_FILE)
CPPFLAGs = -E -S
OBJS = $(SOURCES:.c=.o)
# Compiler Flags and Defines
	ifeq ($(PLATFORM) ,HOST)
		CC = gcc
		LD = -ld
	else
		CC = arm-none-eabi-gcc
		# Architectures Specific Flags
		LINKER_FILE = -T msp432p401r.lds
		CPU = cortex-m4
		ARCH = armv7e-m
		SPECS = nosys.specs
	endif
CFLAGS = -std=c99 -Wall -Werror -O0 -g -D$(PLATFORM) $(INCLUDES)

.PHONY: all
all: $(TARGET).out


%.i:$(SOURCES)
	$(CC) $(CFLAGS) $(CPPFLAGs) $< -o $@

%.o:$(SOURCES)
	$(CC) $(CFLAGS) $^ -o $@

%.asm:$(SOURCES)
	$(CC) $(CFLAGS)  $(CPPFLAGs) -o $@ $^

$(TARGET).out:$(OBJS)
	$(CC) $(CFLAGS) $(OBJS) -o $@

.PHONY: clean
clean:
	rm -f $(OBJS) $(TARGET).out $(TARGET).map *.i *.asm

.PHONY: build
build: all


