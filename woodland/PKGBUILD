# Maintainer: Lex Black <autumn-wind@web.de>

pkgname=woodland
pkgver=2.0.4
pkgrel=1
pkgdesc="minimal Wayland compositor based on wlroots"
url="https://github.com/DiogenesN/woodland"
arch=('x86_64')
license=('GPL-2.0-or-later')
depends=(
    'cairo'
    'dbus'
    'gdk-pixbuf2'
    'glibc'
    'glib2'
    'libdrm'
    'libinput'
    'librsvg'
    'libwlroots-0.18.so'
    'libxkbcommon'
    'libxml2'
    'pixman'
    'wayland'
)
makedepends=('stb')
source=(${pkgname}-${pkgver}.tar.gz::https://github.com/DiogenesN/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz
        0001_adj-makefile.patch)
b2sums=('a555dca150d420105e644bcc5cb727b8c925a81efd09e1bb772e7738d1cda771f056ba15a73dd101e82e856ace046627c80acdb848a8ff0fb91b4661f5e4ea4e'
        'cf852b0fe89780df03c8dd9e2dc6703566f429494b8ce18e52861cd4012a569577586bbbcafea4a9fa241182e917e4a0ed61e100957efd7596b45d3690b32dd8')


prepare() {
  cd $pkgname-$pkgver
  patch -Np2 -i "${srcdir}"/0001_adj-makefile.patch
}

build() {
  cd $pkgname-$pkgver
  cp -v Makefile.in Makefile
  make PREFIX="/usr"
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" PREFIX="/usr" install
}

