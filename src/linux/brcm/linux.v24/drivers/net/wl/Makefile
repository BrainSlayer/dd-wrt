#
# Makefile for the Broadcom wl driver
#
# Copyright 2004, Broadcom Corporation
# All Rights Reserved.
# 
# THIS SOFTWARE IS OFFERED "AS IS", AND BROADCOM GRANTS NO WARRANTIES OF ANY
# KIND, EXPRESS OR IMPLIED, BY STATUTE, COMMUNICATION OR OTHERWISE. BROADCOM
# SPECIFICALLY DISCLAIMS ANY IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS
# FOR A SPECIFIC PURPOSE OR NONINFRINGEMENT CONCERNING THIS SOFTWARE.
#
# $Id: Makefile,v 1.2 2005/03/29 03:32:18 mbm Exp $

EXTRA_CFLAGS += -I$(TOPDIR)/arch/mips/bcm947xx/include -DBCMDRIVER=1 -DBCMDMA64=1

O_TARGET	:= wl.o

obj-$(CONFIG_APSTAMIMO)		:= wl_apsta_mimo.o
obj-$(CONFIG_APSTA)		:= wl_apsta.o

obj-y		+= bcmutils.o hnddma.o linux_osl.o

obj-m		:= $(O_TARGET)
export-objs	:= bcmutils.o
#wl_mod.o: wl_apsta.o
#	sed -e 's,eth%d,wl%d\x00,g' < $< > $@

wl_link.o: wl.o
	$(OBJDUMP) -d $< | perl patchtable.pl > patchtable.bin
	cat wl.o patchtable.bin > $@
	cp wl_link.o wl.o

modules: wl_link.o

include $(TOPDIR)/Rules.make
