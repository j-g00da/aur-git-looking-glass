# Maintainer: Leandro Guedes <leanguedes at icloud dot com>

pkgname=keepsecret-git
pkgver=r231.6483fa1
pkgrel=1
pkgdesc='Password manager for viewing, editing, creating, or deleting passwords'
arch=(x86_64)
url='https://apps.kde.org/keepsecret/'
license=(GPL-2.0-or-later)
depends=(gcc-libs
         glib2
         glibc
         kconfig
         kcoreaddons
         kdbusaddons
         ki18n
         kirigami
         kirigami-addons
         kitemmodels
         libsecret
         qqc2-desktop-style
         qt6-base
         qt6-declarative
         qt6-svg)
makedepends=(extra-cmake-modules
             git
             kdoctools
             vulkan-headers)
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=(git+https://invent.kde.org/utilities/keepsecret.git)
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/${pkgname%-git}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cmake -B build -S ${pkgname%-git} \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
