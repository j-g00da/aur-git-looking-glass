# Maintainer: Andrew O'Neill <andrew at haunted dot sh>

pkgname=simdzone
pkgver=0.2.4
pkgrel=1
pkgdesc='Fast and standards compliant DNS presentation format parser'
arch=('x86_64')
url="https://github.com/NLnetLabs/${pkgname}"
license=('BSD')
makedepends=('cmake')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('2c0189039935e60477165950e3e78f9cfb7cf8c9aeeb4e70f9b5b02383dab8e7')

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
  install -Dm755 build/zone-bench "${pkgdir}"/usr/bin/zone-bench
  install -Dm644 "${pkgname}-${pkgver}"/LICENSE "${pkgdir}"/usr/share/licenses/"${pkgname}"/LICENSE
}
