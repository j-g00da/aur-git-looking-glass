pkgname=flutterup
pkgver=0.2.4
pkgrel=1.0
pkgdesc='A flutter wrapper, to install and package flutter packages'
arch=('x86_64' 'aarch64')
url='https://github.com/Decodetalkers/flutterup'
license=('MIT')
provides=('flutter' 'dart')
conflicts=('flutter' 'dart')
depends=('git' 'ninja')
makedepends=('git' 'ninja' 'meson' 'rust')
source=("flutterup-v${pkgver}.tar.gz::https://github.com/Decodetalkers/flutterup/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('ad98da098db44ea52d05df112b3e8ed55020479cd200cb9b11bb5a82c3f7f5e5')

build() {
  cd ${pkgname}-$pkgver
  meson setup \
    -Dprefix=/usr \
    -Dbuildtype=release \
    build
  ninja -C build
}

package() {
  cd ${pkgname}-$pkgver
  DESTDIR="$pkgdir" ninja -C build install
}
