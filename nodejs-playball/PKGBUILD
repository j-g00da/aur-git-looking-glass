# Maintainer: Brandon Mittman <brandonmittman@gmail.com>
_npmname=playball
_npmver=3.2.0
pkgname=nodejs-playball # All lowercase
pkgver=3.2.0
pkgrel=1
pkgdesc="Watch MLB games from the comfort of your terminal"
arch=(any)
url="https://github.com/paaatrick/playball"
license=(MIT)
depends=('nodejs' 'npm')
optdepends=()
source=(https://registry.npmjs.org/$_npmname/-/$_npmname-$_npmver.tgz)
noextract=($_npmname-$_npmver.tgz)
sha1sums=(230feb7eabfb988ef3e77f915e305807a7814461)

package() {
  cd $srcdir
  local _npmdir="$pkgdir/usr/lib/node_modules/"
  mkdir -p $_npmdir
  cd $_npmdir
  npm install -g --prefix "$pkgdir/usr" $_npmname@$_npmver
  chown -R root:root "$pkgdir"
}

# vim:set ts=2 sw=2 et:
