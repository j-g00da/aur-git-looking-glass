# Maintainer:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: Christian Krause ("wookietreiber") <christian.krause@mailbox.org>

pkgname=mothur
pkgver=1.48.4
pkgrel=1
pkgdesc='A bioinformatics program for analyzing microbial communities.'
arch=('x86_64')
url='https://www.mothur.org/'
license=('GPL-3.0-only')
depends=('boost-libs')
options=('!debug')
makedepends=('boost' 'hdf5')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/${pkgname}/${pkgname}/archive/v${pkgver}.tar.gz")
sha256sums=('aa0de1133fa554f91f861ba01bc63212236d66a7b414b7edea5729987350eca2')

prepare() {
  cd "${pkgname}-${pkgver}"

  sed -i '13 i \#include <memory>' source/writer.h
  sed -i '123d' Makefile
  sed -i '124d' Makefile
}

build() {
  cd "${pkgname}-${pkgver}"

  make
}

package() {
  cd "${pkgname}-${pkgver}"

  install -Dm755 mothur "${pkgdir}/usr/bin/mothur"
  install -Dm755 uchime "${pkgdir}/usr/bin/uchime"
}
