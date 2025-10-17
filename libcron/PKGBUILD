# Maintainer: hellopoisonx <x1665341912@gmail.com>
# Contributor: Atom Long <atom.long@hotmail.com>

pkgname=libcron
pkgver=1.3.1
pkgrel=1
pkgdesc='A C++ scheduling library using cron formatting.'
url='https://github.com/PerMalmberg/libcron'
arch=('x86_64' 'i686' 'arm' 'armv6h' 'armv7h' 'aarch64')
license=('MIT')
conflicts=("${pkgname}-git")
_date_ver=3.0.3
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz"
        "date-${_date_ver}.tar.gz::https://github.com/HowardHinnant/date/archive/refs/tags/v${_date_ver}.tar.gz")
sha256sums=('cf5af6af392df29c8fc61fcc5a8e452118f31f47d7aa92eb7d4f4183dea227c8'
            '30de45a34a2605cca33a993a9ea54e8f140f23b1caf1acf3c2fd436c42c7d942')
makedepends=('cmake')

prepare() {
  cd ${pkgname}-${pkgver}
  cp -rf "${srcdir}/date-${_date_ver}" -T libcron/externals/date
}

build() {
  cd ${pkgname}-${pkgver}
  cmake -DCMAKE_BUILD_TYPE=Release .
  make libcron
}

package() {
  cd ${pkgname}-${pkgver}
  install -Dm644 libcron/out/Release/liblibcron.a -t ${pkgdir}/usr/lib/
  install -Dm644 libcron/include/libcron/* -t ${pkgdir}/usr/include/libcron/
  install -Dm644 libcron/externals/date/include/date/* -t ${pkgdir}/usr/include/date/
}
