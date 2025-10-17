# Maintainer:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: EndlessEden <eden [at] rose.place>
# Contributor: Juri Grabowski <arch-dablin-maint@jugra.de>

pkgname=dablin
pkgver=1.16.1
pkgrel=1
pkgdesc='Plays a DAB/DAB+ audio service from a live transmission or from a stored ensemble recording'
arch=('x86_64')
url="https://github.com/Opendigitalradio/${pkgname}"
license=('GPL-3.0-only')
depends=('sdl2' 'mpg123' 'gtkmm3' 'faad2')
makedepends=('cmake')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/${pkgver}.tar.gz")
sha256sums=('1cc2daa60b6df6a296d0d2b1826de5a78dc007fa08e6895d85a915630fbea9ea')

build() {
  local cmake_options=(
    -B build
    -S "${pkgname}-${pkgver}"
    -W no-dev
    -D CMAKE_BUILD_TYPE=Release
    -D CMAKE_INSTALL_PREFIX=/usr
  )

  cmake "${cmake_options[@]}"
  cmake --build build
}

package() {
  DESTDIR="${pkgdir}" cmake --install build
}
