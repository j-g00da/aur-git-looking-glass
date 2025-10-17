# Maintainer: Leandro Guedes <leanguedes at icloud dot com>

pkgname=komodo-git
pkgver=1.5.0.r4.4a056fa
pkgrel=1
pkgdesc='A todo manager that uses todo.txt specification'
arch=(x86_64)
url='https://apps.kde.org/komodo/'
license=(GPL-2.0-or-later)
depends=(gcc-libs
         glibc
         kcolorscheme
         kconfig
         kcoreaddons
         kdbusaddons
         kguiaddons
         ki18n
         kiconthemes
         kirigami
         kirigami-addons
         kitemmodels
         qqc2-desktop-style
         qt6-base
         qt6-declarative)
makedepends=(extra-cmake-modules
             git
             kdoctools)
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=(git+https://invent.kde.org/utilities/komodo.git)
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/${pkgname%-git}"
  printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}

build() {
  cmake -B build -S ${pkgname%-git}
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
