CC=			gcc
CFLAGS=		-W -O2 -Wall -fomit-frame-pointer
DFLAGS=		#-DUSE_KR_ALLOC
LIBOBJS=	aa2nt.o aa2nt_local.o transaln.o \
			splice.o splice_local.o splice_bound.o \
			common_align.o \
			seq.o table.o align.o \
			pwalign.o
EXEOBJS=	pwalign_main.o ../common/mem.o
SMEXEOBJS=	make_matrix.o
INCLUDES=	-I..

.SUFFIXES:.c .o

.c.o:
		$(CC) -c $(CFLAGS) $(DFLAGS) $< -o $@ $(INCLUDES) -I..

all:pwalign

lib:libalign.a

install:

libalign.a:$(LIBOBJS)
		$(AR) -cru $@ $(LIBOBJS)

pwalign:libalign.a $(EXEOBJS)
		$(CC) $(CFLAGS) $(DFLAGS) $(EXEOBJS) -L. -lalign -o $@

make_matrix.o:gen_nt_sm.c
		$(CC) -c $(CFLAGS) $(DFLAGS) -DALN_MATRIX_DEBUG gen_nt_sm.c -o $@ $(INCLUDES)

make_matrix: $(SMEXEOBJS)
		$(CC) $(CFLAGS) $(DFLAGS) $(SMEXEOBJS) -o $@ -lm $(INCLUDES)

clean:
		rm -f *.o common/*.o libalign.a pwalign gmon.out a.out make_matrix
