.PHONY: check clean distribution

OBJECTS=ck_stack ck_epoch_synchronize ck_epoch_poll
HALF=`expr $(CORES) / 2`

all: $(OBJECTS)

check: all
	./ck_stack $(CORES) 1
	./ck_epoch_synchronize $(HALF) $(HALF) 1
	./ck_epoch_poll $(CORES) 1 1

ck_epoch_synchronize: ck_epoch_synchronize.c ../../../include/ck_stack.h ../../../include/ck_epoch.h ../../../src/ck_epoch.c
	$(CC) $(CFLAGS) -o ck_epoch_synchronize ck_epoch_synchronize.c ../../../src/ck_epoch.c

ck_epoch_poll: ck_epoch_poll.c ../../../include/ck_stack.h ../../../include/ck_epoch.h ../../../src/ck_epoch.c
	$(CC) $(CFLAGS) -o ck_epoch_poll ck_epoch_poll.c ../../../src/ck_epoch.c

ck_stack: ck_stack.c ../../../include/ck_stack.h ../../../include/ck_epoch.h ../../../src/ck_epoch.c
	$(CC) $(CFLAGS) -o ck_stack ck_stack.c ../../../src/ck_epoch.c

clean:
	rm -rf *~ *.o $(OBJECTS) *.dSYM

include ../../../build/regressions.build
CFLAGS+=$(PTHREAD_CFLAGS) -D_GNU_SOURCE
