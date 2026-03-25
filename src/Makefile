MK	= make
SUBDIRS	= hypoDD ncsn2pha ph2dt

# Auto-detect platform: x86_64 Linux uses large arrays + mcmodel=large
# ARM64 (macOS Apple Silicon) uses small arrays, no mcmodel
ARCH := $(shell uname -m)
OS   := $(shell uname -s)

ifeq ($(ARCH),x86_64)
  SIZE ?= large
  MCMODEL = -mcmodel=large
  LDFLAGS_EXTRA =
else
  # ARM64 macOS or other
  SIZE ?= small
  MCMODEL =
  LDFLAGS_EXTRA =
endif

# Allow override: make all SIZE=large  or  make all SIZE=small
export MCMODEL

INCLDIR = ../include

all: setup_includes
	for d in $(SUBDIRS); do (cd $$d; echo $$d; $(MK) $@); done

setup_includes:
	@echo "Platform: $(OS) $(ARCH), SIZE=$(SIZE), MCMODEL=$(MCMODEL)"
	@cp $(INCLDIR)/hypoDD.inc.$(SIZE) $(INCLDIR)/hypoDD.inc
	@cp $(INCLDIR)/ph2dt.inc.$(SIZE) $(INCLDIR)/ph2dt.inc

clean:
	for d in $(SUBDIRS); do (cd $$d; echo $$d; $(MK) $@); done
