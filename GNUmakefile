PREFIX	:= /usr/local

PROG     := tetris
SRCS     := input.c scores.c screen.c shapes.c tetris.c
OBJS     := input.o scores.o screen.o shapes.o tetris.o
MAN      := tetris.6

DEPS     := ncurses libbsd-overlay
#CPPFLAGS += -D_GNU_SOURCE -D__dead= -DOXTABS=XTABS -D"unveil(...)=0" -D"pledge(...)=0"
CPPFLAGS += -D_GNU_SOURCE -D__dead= -DOXTABS=XTABS
CFLAGS   += $(shell pkg-config --cflags $(DEPS))
LDLIBS   += $(shell pkg-config --libs $(DEPS))

COSMO_LIBDIR := ./libcosmo

CFLAGS   += -O0 -g -Wall -Wno-strict-prototypes -Wno-unused-value \
      -std=c99 -static \
      -fno-pie -fno-omit-frame-pointer \
      -mno-red-zone -pg \
      -nostdinc -nostdlib \
      -Iheader_stubs/ \
      -include $(COSMO_LIBDIR)/cosmopolitan.h

LDFLAGS  := -static -nostdlib -nostdinc \
      -fno-pie -mno-red-zone \
      -include $(COSMO_LIBDIR)/cosmopolitan.h \

LIBS     := -fuse-ld=bfd \
      -Wl,-T,$(COSMO_LIBDIR)/ape.lds \
      -include $(COSMO_LIBDIR)/cosmopolitan.h \
      $(COSMO_LIBDIR)/crt.o \
      $(COSMO_LIBDIR)/ape.o \
      $(COSMO_LIBDIR)/cosmopolitan.a


all: $(PROG)

$(PROG): $(OBJS)

clean:
	-$(RM) $(OBJS) $(PROG)
