# Maintainer: Andy Alt <arch_stanton5995 at proton.me>
# Contributor: Oliver Jaksch <arch-aur at com-in dot de>

pkgname=rmw
pkgver=0.9.4
pkgrel=1
pkgdesc="trash/recycle bin utility for the command line"
arch=('i686' 'x86_64' 'aarch64')
url="https://theimpossibleastronaut.com/rmw-website/"
license=('GPL-3.0-or-later')
depends=('glibc' 'ncurses')
makedepends=('meson' 'ninja')
optdepends=('gettext' 'canfigger')

source=("https://github.com/theimpossibleastronaut/rmw/releases/download/v${pkgver}/${pkgname}-${pkgver}.tar.xz")
sha256sums=('81c6b7f1868695f4662be45a5e645fd149fda362e8ec1a822d74d735735ba808')

build() {
  arch-meson $pkgname-$pkgver build -Db_sanitize=none
  meson compile -v -C build
}

package() {
  DESTDIR="$pkgdir" meson install -C build
}
