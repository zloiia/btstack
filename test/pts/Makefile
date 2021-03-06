# Makefile for libusb based PTS tests
BTSTACK_ROOT = ../..
POSIX_ROOT= ${BTSTACK_ROOT}/platforms/posix

CORE += main.c stdin_support.c

COMMON += hci_transport_h2_libusb.c run_loop_posix.c remote_device_db_fs.c


include ${BTSTACK_ROOT}/example/embedded/Makefile.inc

CFLAGS += -I${POSIX_ROOT}/src -I${BTSTACK_ROOT}/platforms/libusb
# CC = gcc-fsf-4.9
CFLAGS  += -g -Wall 
# CFLAGS += -Werror

VPATH += ${BTSTACK_ROOT}/platforms/posix/src
VPATH += ${BTSTACK_ROOT}/platforms/libusb

# use pkg-config
CFLAGS  += $(shell pkg-config libusb-1.0 --cflags)
LDFLAGS += $(shell pkg-config libusb-1.0 --libs)

EXAMPLES = ble_peripheral_test ble_central_test l2cap_test ancs_client classic_test bnep_test hsp_ag_test hsp_hs_test

all: ${BTSTACK_ROOT}/include/btstack/version.h ${EXAMPLES}

ble_peripheral_test: profile.h ${CORE_OBJ} ${COMMON_OBJ} ${ATT_OBJ} ${GATT_SERVER_OBJ} ${SM_REAL_OBJ} ble_peripheral_test.o
	${CC} $(filter-out profile.h,$^) ${CFLAGS} ${LDFLAGS} -o $@

ble_central_test: ${CORE_OBJ} ${COMMON_OBJ} ${SM_REAL_OBJ} ${ATT_OBJ}  ${GATT_CLIENT_OBJ}  ble_central_test.c
	${CC} $^ ${CFLAGS} ${LDFLAGS} -o $@

hsp_ag_test: ${CORE_OBJ} ${COMMON_OBJ} ${SDP_CLIENT} hsp_ag.o hsp_ag_test.c 
	${CC} $^ ${CFLAGS} ${LDFLAGS} -o $@

hsp_hs_test: ${CORE_OBJ} ${COMMON_OBJ} ${SDP_CLIENT} hsp_hs.o hsp_hs_test.c  
	${CC} $^ ${CFLAGS} ${LDFLAGS} -o $@

l2cap_test: ${CORE_OBJ} ${COMMON_OBJ} l2cap_test.c
	${CC} $^ ${CFLAGS} ${LDFLAGS} -o $@

classic_test: ${CORE_OBJ} ${COMMON_OBJ} ${SDP_CLIENT} classic_test.c
	${CC} $^ ${CFLAGS} ${LDFLAGS} -o $@

bnep_test: ${CORE_OBJ} ${COMMON_OBJ} bnep_test.c
	${CC} $^ ${CFLAGS} ${LDFLAGS} -o $@
