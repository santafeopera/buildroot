BUILDROOT_HOME=/home/petonic/br/2018-05-v3-sfe

CC=$(BUILDROOT_HOME)/output/host/usr/bin/arm-linux-gcc
CFLAGS=--sysroot=$(BUILDROOT_HOME)/output/staging
INCLUDES=
LFLAGS=

LIBS=

SRC=chw.c
OBJ=$(SRC:.c=.o)
MAIN=chw

RM=rm -rf

.c.o:
	$(CC) $(CFLAGS) $(INCLUDES) -c $(SRC) -o $@

$(MAIN): $(OBJ)
	$(CC) $(CFLAGS) $(INCLUDES) -o $(MAIN) $(OBJ) $(LFLAGS) $(LIBS)

all: $(MAIN)

clean:
	$(RM) $(MAIN) *.o *~
