# Maintainer: Lex Black <autumn-wind@web.de>

pkgname=havoc
pkgver=0.7.0
pkgrel=1
pkgdesc='minimal terminal emulator for Wayland on Linux'
arch=(x86_64)
url='https://github.com/ii8/havoc'
license=('MIT')
depends=(libxkbcommon wayland)
makedepends=('wayland-protocols')
source=(${pkgname}-${pkgver}.tar.gz::https://github.com/ii8/havoc/archive/${pkgver}.tar.gz)
b2sums=('7204efcfdcf6ec6a5cbe70a39f122c66fc8788462739f9cf052f20c9c0933ab58de559f5c179e1394ec4dc9acb0c761d9c4f14459949d24ad4613bdfb0767042')


build() {
  cd ${pkgname}-${pkgver}
  make PREFIX=/usr
}

package() {
  cd ${pkgname}-${pkgver}
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  make PREFIX=/usr DESTDIR="${pkgdir}" install
}
