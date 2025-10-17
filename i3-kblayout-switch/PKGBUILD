pkgname=i3-kblayout-switch
pkgver=1.0
pkgrel=1
pkgdesc="Remembers keyboard layout per i3 workspace"
options=(!debug)
arch=('any')
url="https://github.com/f0s3/i3-kblayout-switch"
license=('MIT')
depends=('bun-bin' 'xkb-switch' 'xkblayout-state')
makedepends=('bun-bin' 'xkb-switch' 'xkblayout-state')
source=("$pkgname-$pkgver.tar.gz::https://github.com/f0s3/$pkgname/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('5cbb3e2d20af7f079676c92647072323dbb47782e2e4ffac0ee7b5ea59dad6b9')

build() {
  return 0
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  install -Dm755 i3-kblayout-switch.ts "$pkgdir/usr/bin/i3-kblayout-switch"
}
