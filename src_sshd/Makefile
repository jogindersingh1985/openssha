# $Id: Makefile.in,v 1.297 2008/07/08 14:21:12 djm Exp $

# uncomment if you run a non bourne compatable shell. Ie. csh
#SHELL = /bin/sh

AUTORECONF=autoreconf

#prefix=/usr/local
prefix=/sshd
exec_prefix=${prefix}
bindir=${exec_prefix}/bin
sbindir=${exec_prefix}/sbin
libexecdir=${exec_prefix}/libexec
datadir=${datarootdir}
datarootdir=${prefix}/share
mandir=${datarootdir}/man
mansubdir=man
sysconfdir=${prefix}/etc1
#sysconfdir=./config
piddir=/var/run
srcdir=.
top_srcdir=.

DESTDIR=

SSH_PROGRAM=${exec_prefix}/bin/ssh
ASKPASS_PROGRAM=$(libexecdir)/ssh-askpass
SFTP_SERVER=$(libexecdir)/sftp-server
SSH_KEYSIGN=$(libexecdir)/ssh-keysign
RAND_HELPER=$(libexecdir)/ssh-rand-helper
PRIVSEP_PATH=/var/empty
SSH_PRIVSEP_USER=sshd
STRIP_OPT=-s

PATHS= -DSSHDIR=\"$(sysconfdir)\" \
	-D_PATH_SSH_PROGRAM=\"$(SSH_PROGRAM)\" \
	-D_PATH_SSH_ASKPASS_DEFAULT=\"$(ASKPASS_PROGRAM)\" \
	-D_PATH_SFTP_SERVER=\"$(SFTP_SERVER)\" \
	-D_PATH_SSH_KEY_SIGN=\"$(SSH_KEYSIGN)\" \
	-D_PATH_SSH_PIDDIR=\"$(piddir)\" \
	-D_PATH_PRIVSEP_CHROOT_DIR=\"$(PRIVSEP_PATH)\" \
	-DSSH_RAND_HELPER=\"$(RAND_HELPER)\"

CC=gcc
LD=gcc
CFLAGS=-g -Wall -Wpointer-arith -Wuninitialized -Wsign-compare -Wformat-security -fno-builtin-memset -std=gnu99 
CPPFLAGS=-I. -I/usr/local/ssl/include -I$(srcdir) -I../ $(PATHS) -DHAVE_CONFIG_H
LIBS=-lresolv -lcrypto -lutil -lz -lnsl  -ldl -lcrypt
SSHDLIBS=
LIBEDIT=
AR=/usr/bin/ar
AWK=gawk
RANLIB=ranlib
INSTALL=/usr/bin/install -c
PERL=/usr/bin/perl
SED=/bin/sed
ENT=
XAUTH_PATH=undefined
LDFLAGS=-L. -L/usr/local/ssl/lib/ -L../ -L../openbsd-compat/ 
EXEEXT=

TARGETS=sshd$(EXEEXT)

#LIBSSH_OBJS=acss.o authfd.o authfile.o bufaux.o bufbn.o buffer.o \
	canohost.o channels.o cipher.o cipher-acss.o cipher-aes.o \
	cipher-bf1.o cipher-ctr.o cipher-3des1.o cleanup.o \
	compat.o compress.o crc32.o deattack.o fatal.o hostfile.o \
	log.o match.o md-sha256.o moduli.o nchan.o packet.o \
	readpass.o rsa.o ttymodes.o xmalloc.o addrmatch.o \
	atomicio.o key.o dispatch.o kex.o mac.o uidswap.o uuencode.o misc.o \
	monitor_fdpass.o rijndael.o ssh-dss.o ssh-rsa.o dh.o kexdh.o \
	kexgex.o kexdhc.o kexgexc.o scard.o msg.o progressmeter.o dns.o \
	entropy.o scard-opensc.o gss-genr.o umac.o

#SSHDOBJS=sshd.o auth-rhosts.o auth-passwd.o auth-rsa.o auth-rh-rsa.o \
	sshpty.o sshlogin.o servconf.o serverloop.o \
	auth.o auth1.o auth2.o auth-options.o session.o \
	auth-chall.o auth2-chall.o groupaccess.o \
	auth-skey.o auth-bsdauth.o auth2-hostbased.o auth2-kbdint.o \
	auth2-none.o auth2-passwd.o auth2-pubkey.o \
	monitor_mm.o monitor.o monitor_wrap.o kexdhs.o kexgexs.o \
	auth-krb5.o \
	auth2-gss.o gss-serv.o gss-serv-krb5.o \
	loginrec.o auth-pam.o auth-shadow.o auth-sia.o md5crypt.o \
	audit.o audit-bsm.o platform.o sftp-server.o sftp-common.o

SSHDOBJS=sshd.o auth-rhosts.o auth-passwd.o auth-rsa.o auth-rh-rsa.o \
	sshpty.o sshlogin.o servconf.o serverloop.o \
	auth.o auth1.o auth2.o auth-options.o session.o \
	auth-chall.o auth2-chall.o groupaccess.o \
	auth-skey.o auth-bsdauth.o auth2-hostbased.o auth2-kbdint.o \
	auth2-none.o auth2-passwd.o auth2-pubkey.o \
	kexdhs.o kexgexs.o do_kex2_exchange.o\
	auth-krb5.o \
	auth2-gss.o gss-serv.o gss-serv-krb5.o \
	loginrec.o auth-pam.o auth-shadow.o auth-sia.o md5crypt.o \
	audit.o audit-bsm.o platform.o sftp-server.o sftp-common.o

#CONFIGFILES=sshd_config.out ssh_config.out moduli.out
#CONFIGFILES_IN=sshd_config ssh_config moduli

PATHSUBS	= \
	-e 's|/etc/ssh/ssh_prng_cmds|$(sysconfdir)/ssh_prng_cmds|g' \
	-e 's|/etc/ssh/ssh_config|$(sysconfdir)/ssh_config|g' \
	-e 's|/etc/ssh/ssh_known_hosts|$(sysconfdir)/ssh_known_hosts|g' \
	-e 's|/etc/ssh/sshd_config|$(sysconfdir)/sshd_config|g' \
	-e 's|/usr/libexec|$(libexecdir)|g' \
	-e 's|/etc/shosts.equiv|$(sysconfdir)/shosts.equiv|g' \
	-e 's|/etc/ssh/ssh_host_key|$(sysconfdir)/ssh_host_key|g' \
	-e 's|/etc/ssh/ssh_host_dsa_key|$(sysconfdir)/ssh_host_dsa_key|g' \
	-e 's|/etc/ssh/ssh_host_rsa_key|$(sysconfdir)/ssh_host_rsa_key|g' \
	-e 's|/var/run/sshd.pid|$(piddir)/sshd.pid|g' \
	-e 's|/etc/moduli|$(sysconfdir)/moduli|g' \
	-e 's|/etc/ssh/moduli|$(sysconfdir)/moduli|g' \
	-e 's|/etc/ssh/sshrc|$(sysconfdir)/sshrc|g' \
	-e 's|/usr/X11R6/bin/xauth|$(XAUTH_PATH)|g' \
	-e 's|/var/empty|$(PRIVSEP_PATH)|g' \
	-e 's|/usr/bin:/bin:/usr/sbin:/sbin|/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin|g'

#FIXPATHSCMD	= $(SED) $(PATHSUBS)

all: $(TARGETS)

#$(LIBSSH_OBJS): Makefile.in config.h
$(SSHDOBJS): Makefile.in config.h

.c.o:
	$(CC) $(CFLAGS) $(CPPFLAGS) -c $<

LIBCOMPAT=../openbsd-compat/libopenbsd-compat.a
$(LIBCOMPAT): always
	(cd ../openbsd-compat && $(MAKE))
always:

libssh.a: 
	(cd ../ && $(MAKE))

#libssh.a: $(LIBSSH_OBJS)
#	$(AR) rv $@ $(LIBSSH_OBJS)
#	$(RANLIB) $@

sshd$(EXEEXT): libssh.a	$(LIBCOMPAT) $(SSHDOBJS)
	$(LD) -o $@ $(SSHDOBJS) $(LDFLAGS) -lssh -lopenbsd-compat $(SSHDLIBS) $(LIBS)

# test driver for the loginrec code - not built by default
#logintest: logintest.o $(LIBCOMPAT) libssh.a loginrec.o
#	$(LD) -o $@ logintest.o $(LDFLAGS) loginrec.o -lopenbsd-compat -lssh $(LIBS)

#$(CONFIGFILES): $(CONFIGFILES_IN)
#	conffile=`echo $@ | sed 's/.out$$//'`; \
#	$(FIXPATHSCMD) $(srcdir)/$${conffile} > $@

#ssh_prng_cmds.out:	ssh_prng_cmds
#	if test ! -z "$(INSTALL_SSH_PRNG_CMDS)"; then \
#		$(PERL) $(srcdir)/fixprogs ssh_prng_cmds $(ENT); \
#	fi

# fake rule to stop make trying to compile moduli.o into a binary "moduli.o"
#moduli:
#	echo

#clean:	regressclean
clean:	
	rm -f *.o $(TARGETS)
	rm -f *.out
	(cd ../openbsd-compat && $(MAKE) clean)
	(cd ../ && $(MAKE) clean)

