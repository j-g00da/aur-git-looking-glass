# Maintainer: Leandro Guedes <leanguedes at icloud dot com>

pkgname=libretro-gearsystem
pkgver=1226
pkgrel=1
pkgdesc='Sega Master System/Game Gear/SG-1000 core'
arch=(x86_64)
url=https://github.com/drhelius/Gearsystem
license=(GPL-3.0-or-later)
groups=(libretro)
depends=(libretro-core-info)
makedepends=(git)
_commit=8d83e6abf00ee65a1114e18574c1fe2d1027d143
source=(libretro-gearsystem::git+https://github.com/drhelius/Gearsystem.git#commit=${_commit})
sha256sums=('1f1f3014731e7fdb127e3a33ca8061eed8dabdebf7f0f20eb11eaf6e072ec1bb')

pkgver() {
  cd libretro-gearsystem

  git rev-list --count HEAD
}

build() {
  make -C libretro-gearsystem/platforms/libretro
}

package() {
  install -Dm 644 libretro-gearsystem/platforms/libretro/gearsystem_libretro.so -t "${pkgdir}"/usr/lib/libretro/
  install -Dm 644 libretro-gearsystem/LICENSE -t "${pkgdir}"/usr/share/licenses/libretro-gearsystem/
}

# vim: ts=2 sw=2 et:
