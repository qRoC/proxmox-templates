
BASEDIR:=$(shell dab basedir)

all: info/init_ok
	dab bootstrap --minimal
	dab exec apt-get purge -y postfix rpcbind
	dab exec apt-get update
	dab exec install apt-transport-https ca-certificates locales ntpdate software-properties-common
	echo "en_US.UTF-8" >${BASEDIR}/etc/locale
	echo "en_US.UTF-8 UTF-8" >${BASEDIR}/etc/locale.gen
	dab exec locale-gen
	dab exec rm -rf /etc/localtime
	dab exec ln -s /usr/share/zoneinfo/Europe/Kiev /etc/localtime
	dab exec echo "Europe/Kiev" > /etc/timezone
	sed -e 's/^PermitRootLogin without-password/PermitRootLogin yes/' -i ${BASEDIR}/etc/ssh/sshd_config
	dab exec add-apt-repository -s 'deb http://packages.dotdeb.org jessie all'
	dab exec add-apt-repository -s 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main'
	dab exec wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg
	dab exec wget http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc && apt-key add ACCC4CF8.asc
	dab exec apt-get update
	dab exec install nginx postgresql
	dab exec cp nginx.conf ${BASEDIR}/etc/nginx/nginx.conf
	dab exec cp host.conf ${BASEDIR}/etc/nginx/sites-available/default
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
