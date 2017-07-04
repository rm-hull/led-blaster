AUTOMAKE_OPTIONS = foreign

#CFLAGS = -g -DDEBUG -Wall -pedantic
CFLAGS = -Wall -pedantic -std=c99
EXTRA_DIST = led-blaster.service

sbin_PROGRAMS = led-blaster
pi_blaster_SOURCES = led-blaster.c mailbox.c

if !DEBIAN_PKG
if HAVE_SYSTEMD
systemdsystemunit_DATA = led-blaster.service

# Unless we are cross-compiling, start now.
if !CROSS_COMPILING
install-data-hook:
	systemctl enable led-blaster
	systemctl start led-blaster

uninstall-hook:
	systemctl stop led-blaster
	systemctl disable led-blaster
endif # !CROSS_COMPILING

else
init_ddir = $(sysconfdir)/init.d
init_d_SCRIPTS = led-blaster.boot.sh

# Unless we are cross-compiling, start now.
if !CROSS_COMPILING
install-data-hook:
	update-rc.d led-blaster.boot.sh defaults
	$(init_ddir)/led-blaster.boot.sh start

uninstall-hook:
	update-rc.d led-blaster.boot.sh remove
	killall led-blaster
endif # !CROSS_COMPILING

endif # !HAVE_SYSTEMD
endif # !DEBIAN_PKG
