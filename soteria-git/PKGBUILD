# Maintainer: Abhinav Chalise <chalisezabhinav at gmail dot com>
pkgname=soteria-git
_pkgname=soteria
pkgver=0.2.0.r2.g9ce1cd4
pkgrel=1
pkgdesc="A GTK-based polkit authentication agent"
arch=('x86_64')
url="https://github.com/imvaskel/soteria"
license=('Apache-2.0')
depends=('gtk4' 'polkit')
makedepends=('git' 'cargo')
options=('!debug')
source=("git+$url#branch=main")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "$srcdir/$_pkgname"
  cargo build --release --locked
}

package() {
  cd "$srcdir/$_pkgname"
  
  install -Dm755 "target/release/$_pkgname" \
    "$pkgdir/usr/lib/soteria-polkit/$_pkgname"

  install -Dm644 LICENSE \
    "$pkgdir/usr/share/licenses/$_pkgname/LICENSE"
}

