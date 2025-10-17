# Maintainer:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: Kevin Slagle <kjslag at gmail dot com>

pkgname=regina-normal
pkgver=7.4
pkgrel=1
pkgdesc='Software for low-dimensional topology'
arch=('x86_64')
url='https://regina-normal.github.io'
license=('GPL-2.0-or-later')
depends=('gmp' 'graphviz' 'jansson' 'libxml2' 'popt' 'python3' 'qt6-base' 'qt6-svg' 'tokyocabinet' 'zlib')
makedepends=('cmake')
optdepends=('doxygen: Generate C++/Python API docs'
	          'cppunit: Build full test suite'
            'libxslt: Generate the user handbook')
source=("https://github.com/${pkgname}/regina/archive/regina-${pkgver}.tar.gz")
sha256sums=('1b76e70982f7ed717b3477c0322d337f7cebf7e228235436b3efb5da3e262c8b')

build() {
  local cmake_options=(
    -B build
    -S "regina-regina-${pkgver}"
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
