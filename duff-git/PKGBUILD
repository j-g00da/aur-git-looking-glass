# Maintainer: Stefan Husmann <stefan-husmann@t-online.de>
# Contributor: Aaron Schaefer <aaron@elasticdog.com>

pkgname=duff-git
pkgver=0.5.2.r60.gc1baefa
pkgrel=2
pkgdesc="A command-line utility for quickly finding duplicates in a given set of files"
arch=('i686' 'x86_64')
url="https://github.com/elmindreda/duff"
license=('custom')
depends=('glibc' 'sh')
makedepends=('git')
conflicts=('duff')
provides=('duff')
source=("git+https://github.com/elmindreda/${pkgname%-git}.git")
md5sums=('SKIP')

pkgver() {
  cd ${pkgname%-git}
  git describe --tags | sed 's+-+.r+' | tr - .
}

prepare() {
  cd ${pkgname%-git}

  # How to avoid the manual confirmation?
  gettextize --no-changelog -f

  # https://github.com/elmindreda/duff/issues/17
  sed -i 's#po/Makefile.in##' configure.ac

  autoreconf -fiv

  # https://github.com/elmindreda/duff/issues/18
  sed -i 's/ö/oe/g' src/duff.c
}

build() {
  cd ${pkgname%-git}
  ./configure --prefix=/usr --mandir=/usr/share/man
  make
}

package() {
  cd ${pkgname%-git}
  make DESTDIR="$pkgdir" install
  install -D -m644 COPYING "$pkgdir"/usr/share/licenses/${pkgname}/COPYING
}

