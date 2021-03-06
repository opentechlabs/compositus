CC=gcc
CFLAGS=-Wall -std=c99 -O2 -g -Wp,-D_FORTIFY_SOURCE=2 -D_FILE_OFFSET_BITS=64 -fexceptions -fstack-protector --param=ssp-buffer-size=4 -fPIE
LDFLAGS=-Wl,-z,now -pie
LIBS=-L../../libctemplate `pkg-config --libs glib-2.0` `pkg-config --libs gmime-2.0` `mysql_config --libs` -lm -pthread -lrt -lcrypt -lfcgi -lmhash -ltokyocabinet -lctemplate-fcgi
INCS=-I../../libctemplate `pkg-config --cflags glib-2.0` `pkg-config --cflags gmime-2.0` `mysql_config --cflags`

objects = compositus.o get_config.o url_handlers.o utils.o db.o audit.o csrf.o

compositus: $(objects)
	@echo -e "  LNK\t$@"
	@$(CC) $(LDFLAGS) -o compositus $(objects) ${LIBS}

compositus.o: common.h get_config.h compositus_config.h url_handlers.h compositus.h compositus.c
	@echo -e "  CC\t$@"
	@$(CC) $(CFLAGS) -c compositus.c ${INCS}

url_handlers.o: common.h utils.h audit.h url_handlers.c
	@echo -e "  CC\t$@"
	@$(CC) $(CFLAGS) -c url_handlers.c ${INCS}

utils.o: common.h utils.h utils.c
	@echo -e "  CC\t$@"
	@$(CC) $(CFLAGS) -c utils.c ${INCS}

db.o: common.h compositus_config.h utils.h db.h db.c
	@echo -e "  CC\t$@"
	@$(CC) $(CFLAGS) -c db.c ${INCS}

get_config.o: compositus_config.h common.h get_config.c
	@echo -e "  CC\t$@"
	@$(CC) $(CFLAGS) -c get_config.c ${INCS}

audit.o: common.h utils.h audit.c
	@echo -e "  CC\t$@"
	@$(CC) $(CFLAGS) -c audit.c ${INCS}

csrf.o: common.h utils.h csrf.c
	@echo -e "  CC\t$@"
	@$(CC) $(CFLAGS) -c csrf.c ${INCS}

clean:
	rm -f compositus *.o
