# Maintainer: Andrew O'Neill <andrew at haunted dot sh>

_pkgname=mini
pkgname=cpp-${_pkgname}
pkgver=0.9.18
pkgrel=1
pkgdesc="Tiny, header only C++ library for manipulating INI files."
arch=('any')
license=('MIT')
conflicts=('mini-git')
url="https://github.com/metayeti/mINI"
source=("${_pkgname}-${pkgver}.tar.gz::${url}/archive/${pkgver}.tar.gz")
sha256sums=('53b06f2dfbc79f6c5317636dbd61d29f27bb2c98629743bb6bf83b919d1bc657')

package() {
  cd "mINI-${pkgver}"

  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
  install -D -m644 src/mini/ini.h "${pkgdir}/usr/include/mini/ini.h"
}
