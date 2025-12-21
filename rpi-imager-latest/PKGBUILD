pkgname=rpi-imager-latest
pkgver=2.0.2
pkgrel=1
pkgdesc="Raspberry Pi Imager – flash images to SD cards and USB drives"
arch=(x86_64 aarch64)
url="https://www.raspberrypi.com/software/"
license=(Apache)
depends=(
  qt6-base
  qt6-svg
  qt6-tools
  libarchive
  curl
  hicolor-icon-theme
)
makedepends=(
  cmake
  qt6-tools
)
provides=('rpi-imager')
conflicts=('rpi-imager-git')
source=(
  "$pkgname-$pkgver.tar.gz::https://github.com/raspberrypi/rpi-imager/archive/refs/tags/v$pkgver.tar.gz"
)
sha256sums=('cc3b784705ca0638eff8b9dc976eb9a02892bf5076d95b4af9f7f355a17326f6')

prepare() {
  # Patch CMakeLists.txt to force the correct version
  cd "$srcdir/rpi-imager-$pkgver/src"
  sed -i "s|0.0.0-unknown|$pkgver|g" CMakeLists.txt
}

build() {
  cmake -B build -S "$srcdir/rpi-imager-$pkgver/src" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DUSE_SYSTEM_LIBARCHIVE=ON \
    -DUSE_SYSTEM_CURL=ON
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}

