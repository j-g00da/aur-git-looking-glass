# Maintainer: Lex Black <autumn-wind@web.de>
# Contributor: Firegem <mrfiregem [at] protonmail [dot] ch>

pkgname=wlopm-git
pkgver=1.0.0.r1.g41bc661
pkgrel=2
pkgdesc="Wayland output power management."
arch=('x86_64')
url="https://git.sr.ht/~leon_plickat/wlopm"
license=('GPL-3.0-only')
depends=(wayland)
makedepends=('git' 'wayland-protocols')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=('git+https://git.sr.ht/~leon_plickat/wlopm')
md5sums=('SKIP')

pkgver() {
  cd "${pkgname%-git}"
  git describe --long --abbrev=7 | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${pkgname%-git}"
  make PREFIX='/usr' DESTDIR="$pkgdir"
}

package() {
  cd "${pkgname%-git}"
  make install PREFIX='/usr' DESTDIR="$pkgdir"
}
