# Maintainer: Breno Ramalho Lemes <breno@br-lemes.net>
pkgname=php-firebird
pkgver=8.4.15
pkgrel=1
pkgdesc='Firebird module for PHP'
arch=('x86_64')
url='http://www.php.net'
license=('PHP-3.01')
depends=("php=${pkgver}" 'glibc' 'libfbclient')
source=("https://php.net/distributions/php-${pkgver}.tar.xz"
	'pdo_firebird.ini')
sha256sums=('a060684f614b8344f9b34c334b6ba8db1177555997edb5b1aceab0a4b807da7e'
	'41187271bb8a552ff10c997bc31557f9f09f47087618fde0c08e3304e204b771')

build() {
	cd ${srcdir}/php-${pkgver}/ext/pdo_firebird
	phpize
	./configure --with-pdo-firebird=/usr/lib/php/modules
	make
}

package() {
	mkdir -p "$pkgdir"/{/usr/lib/php/modules,/etc/php/conf.d}
	install -m755 "$srcdir/php-$pkgver/ext/pdo_firebird/.libs/pdo_firebird.so" "$pkgdir/usr/lib/php/modules"
	install -m644 "$srcdir/pdo_firebird.ini" "$pkgdir/etc/php/conf.d"
}
