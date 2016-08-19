
BASEDIR:=$(shell dab basedir)

all: info/init_ok
	dab bootstrap --minimal
	dab exec apt-get -y purge postfix
	dab exec apt-get update
	dab exec install apt-transport-https ca-certificates locales ntpd
	echo "en_US.UTF-8" >${BASEDIR}/etc/locale
	echo "en_US.UTF-8 UTF-8" >${BASEDIR}/etc/locale.gen
	dab exec locale-gen
	dab exec rm -rf /etc/localtime
	dab exec ln -s /usr/share/zoneinfo/Europe/Kiev /etc/localtime
	dab exec echo "Europe/Kiev" > /etc/timezone
	sed -e 's/^PermitRootLogin without-password/PermitRootLogin yes/' -i ${BASEDIR}/etc/ssh/sshd_config
	dab exec apt-get purge -y postfix rpcbind
	dab finalize

info/init_ok: dab.conf
	dab init
	touch $@

.PHONY: clean
clean:
	dab clean
	rm -f *~

.PHONY: dist-clean
dist-clean:
	dab dist-clean
	rm -f *~
