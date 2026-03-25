CMD	= ph2dt
CC	= gcc
#FC	= g77
#FC	= f77
FC	= gfortran 
SRCS	= $(CMD).f \
	  cluster.f delaz.f ifindi.f \
	  indexx.f indexxi.f sorti.f trimlen.f
CSRCS	= rpad_.c datetime_.c 
OBJS	= $(SRCS:%.f=%.o) $(CSRCS:%.c=%.o)
INCLDIR	= ../../include
# MCMODEL is set by parent Makefile (empty on ARM64, -mcmodel=large on x86_64)
MCMODEL ?=

CFLAGS	= -O -I$(INCLDIR) $(MCMODEL)
LDFLAGS =
FFLAGS  = -I$(INCLDIR) -g $(MCMODEL)

listflg = -L -c -O

# Following line needed on HP-UX (hasn't been tested, though).
#LDFLAGS	= +U77

all: $(CMD)

$(CMD): $(OBJS)
	$(FC) $(LDFLAGS) $(OBJS) $(LIBS) -o $@

%.o: %.f
	$(FC) $(FFLAGS) -c $(@F:.o=.f) -o $@

clean:
	-rm -f $(CMD) *.o core a.out junk

atoangle_.o : ../../include/compat.h
atoangle_.o : ../../include/f77types.h
ph2dt.o : ../../include/ph2dt.inc
