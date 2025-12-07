# Maintainer: Lex Black <autumn-wind@web.de>

pkgname=woodland
pkgver=2.0.5
pkgrel=2
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
b2sums=('add9f118fd0c9244944e69109fccf2fbed3eeb59990659c91f2335f9c71c77bc1ea3f968930dfd371d228f63142d1a2b332e0a630349756cc6dfbb820c103816'
        'e6bf257e56e6d8343a313566be072e116f3cf7f461125286c8cdcc64eb33703160eb39a0a84f78b4d12309f9246b9f95311227254437aac33e9916df93bfe665')


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

