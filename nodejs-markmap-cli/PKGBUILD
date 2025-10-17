# Maintainer: Gregory Danielson III <gregdan3@protonmail.com>

_npmname=markmap-cli
pkgname=nodejs-markmap-cli # All lowercase
pkgver=0.18.7
pkgrel=1
pkgdesc="Create markmaps (mindmaps from markdown) from CLI"
arch=(any)
url="https://markmap.js.org/"
license=(MIT)
depends=('nodejs' 'npm')
optdepends=()
source=(https://registry.npmjs.org/$_npmname/-/$_npmname-$pkgver.tgz)
noextract=($_npmname-$pkgver.tgz)
sha1sums=('a2e2e09422e58cf48afec4987b1fad3507145e12')

package() {
	cd $srcdir
	local _npmdir="$pkgdir/usr/lib/node_modules/"
	mkdir -p $_npmdir
	cd $_npmdir
	npm install -g --prefix "$pkgdir/usr" $_npmname@$pkgver
	chown -R root:root "$pkgdir"
}

# vim:set ts=2 sw=2 et:
