# Contributor: Lex Black <autumn-wind@web.de>

pkgname=wireguard-go
pkgver=0.0.20250522
pkgrel=3
pkgdesc="Go userspace implementation of WireGuard"
arch=('i686' 'pentium4' 'x86_64' 'armv7h' 'armv6h' 'aarch64')
url="https://git.zx2c4.com/wireguard-go/"
license=('MIT')
depends=('glibc')
makedepends=('go')
source=(https://git.zx2c4.com/wireguard-go/snapshot/${pkgname}-${pkgver}.tar.xz
        "0001-go-guidelines.patch")
sha1sums=('01256e3a4539d7bef00638568b4089ce14880c15'
          'e44d694a0db30f5873d4179ac8f80247a16f91b7')


prepare() {
  cd "$pkgname-$pkgver"
  patch -Np2 -i "$srcdir"/0001-go-guidelines.patch
}

build() {
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir"
}

package() {
  cd "$pkgname-$pkgver"
  make DESTDIR="$pkgdir" PREFIX=/usr install

  install -vDm644 LICENSE -t "${pkgdir}"/usr/share/licenses/$pkgname/
}
