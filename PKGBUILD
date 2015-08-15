# Maintainer: smx
pkgname=dualserver
pkgver=7.29
pkgrel=1
pkgdesc="Dual DHCP DNS Server"
arch=('i686' 'x86_64')
url="http://sourceforge.net/projects/dhcp-dns-server"
makedepends=('autoconf' 'automake')
license=('GPL')
source=("http://sourceforge.net/projects/dhcp-dns-server/files/Dual%20DHCP%20DNS%20Server/dualserverV${pkgver}.tar.gz"
		"config.h.in"
		"Makefile.am"
		"configure.ac"
		"dualserverd.service")

md5sums=('bab923614713f5a80ef8ec39981e6784'
         '3e6e71aea694f18f483ab4de2992df20'
         '0417785d29e4a7fa21db1bae737ce94d'
         '28db3256f5ea1294e0c0088cb1d62562'
         '1636730cc2a82c499646af893a90e61b')
		
build() {
	cd ${srcdir}/dualserver
	cp ${srcdir}/config.h.in ${srcdir}/configure.ac ${srcdir}/Makefile.am .
	touch NEWS README AUTHORS ChangeLog
	unset CXXFLAGS CPPFLAGS LDFLAGS DEBUG_CXXFLAGS #we don't want stack protector or other optimziations
	autoreconf --install --force
	./configure CXXFLAGS="-fno-stack-protector" --prefix=/usr \
			--sysconfdir=/etc/dualserver
	make clean
	make
}

package() {
	cd ${srcdir}/dualserver
	make DESTDIR="${pkgdir}" install
	install -D -m0644 ${srcdir}/dualserverd.service "${pkgdir}"/usr/lib/systemd/system/dualserverd.service
}
