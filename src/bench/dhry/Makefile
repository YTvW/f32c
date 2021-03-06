
PROG = dhry

WARNS = 1

# Override -Os, and turn on extra optimization efforts
DHRY_CFLAGS += -Ofast
DHRY_CFLAGS += -fselective-scheduling
DHRY_CFLAGS += -fno-crossjumping

# 1.630 DMIPS/MHz with gcc-6.1
DHRY_CFLAGS += -fipa-pta -fira-algorithm=priority

# Inlining functions is not permitted per Dhrystone rules!
DHRY_CFLAGS += -fno-inline-functions -fno-inline-small-functions
DHRY_CFLAGS += -finline-limit=0

# builtin_strcpy is faster than a handcrafted version
DHRY_CFLAGS += -DUSE_BUILTIN_STRCPY
DHRY_CFLAGS += -DFAST_STRCMP -DUNROLLED_STRCMP

# We don't need floating point support here
WITHOUT_FLOAT = yes

CFILES = dhry_1.c dhry_2.c miscfn.c

# Override default interrupt-driven sio routines
CFILES += ../../lib/src/sio_poll.c

include ${POST_MK}

# Specialized build rules for dhry_*.c files

./obj/${ARCH_DIR}/dhry_1.o: dhry_1.c
	mkdir -p obj/${ARCH_DIR}
	${CC} ${DHRY_CFLAGS} -o $@ dhry_1.c

./obj/${ARCH_DIR}/dhry_2.o: dhry_2.c
	mkdir -p obj/${ARCH_DIR}
	${CC} ${DHRY_CFLAGS} -o $@ dhry_2.c
