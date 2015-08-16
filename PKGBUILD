# Maintainer: Alexey Khromov <zxalexis AT gmail.com>

pkgname=maradns
pkgver=1.4.14
pkgrel=1
pkgdesc="A security-aware DNS server"
arch=('i686' 'x86_64')
depends=(glibc)
source=(http://maradns.samiam.org/download/1.4/$pkgname-$pkgver.tar.gz
		maradns.service
		zoneserver.service
		locations.patch)
md5sums=('96333ef5c69f766284b6fd552b8a4a80'
         '6339458fce452e6973fe897ec0520d28'
         'dd039497df1f4ead054fd3a835885dff'
         '257f42797dee2175dc50f79cca673a4c')
url="http://maradns.org"
license=('custom')

build() {
	install -d ${pkgdir}/usr/{bin,sbin} || return 1
	install -d ${pkgdir}/usr/share/man/man{1,5,8} || return 1
	install -d ${pkgdir}/etc/maradns || return 1
	install -d ${pkgdir}/usr/share/licenses/${pkgname}
	install -d ${pkgdir}/usr/share/doc/${pkgname}
	install -d ${pkgdir}/usr/lib/systemd/system
	
	cd ${srcdir}/${pkgname}-${pkgver}
	patch -p0 < ${startdir}/locations.patch
	make || return 1
	#PREFIX="$pkgdir/usr"
	#RPM_BUILD_ROOT="$PREFIX"
	#make install
	PREFIX=${pkgdir}/usr RPM_BUILD_ROOT=${pkgdir} make install || return 1
	
	install -m755 ${startdir}/maradns.service ${pkgdir}/usr/lib/systemd/system
	install -m755 ${startdir}/zoneserver.service ${pkgdir}/usr/lib/systemd/system
	install -m644 COPYING ${pkgdir}/usr/share/licenses/${pkgname}
}

