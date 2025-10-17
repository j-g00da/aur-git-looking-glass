# Contributor: Lex Black <autumn-wind at web.de>
# Contributor: Deon Spengler <deon at spengler dot co dot za>
# Contributor: magiruuvelvet <contact (at) magiruuvelvet (dot) gdn>

_pkgname=resynthesizer
pkgname=gimp-plugin-resynthesizer
pkgver=3.0
pkgrel=1
pkgdesc="Suite of gimp plugins for texture synthesis"
arch=('x86_64' 'aarch64')
url="https://github.com/bootchk/resynthesizer"
license=('GPL-3.0-only')
depends=('gimp')
makedepends=('meson')
source=("$_pkgname-$pkgver.tar.gz::https://github.com/bootchk/$_pkgname/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('d0f459e551d428e3cd3fec4c3ebfe448e6e2947d9b24553373308d6d41ddd580')


build() {
    arch-meson ${_pkgname}-${pkgver} build
    meson compile -C build
}

package() {
    meson install -C build --destdir "${pkgdir}"
}
