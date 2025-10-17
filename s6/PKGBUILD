# Maintainer:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: Josh VanderLinden <arch@cloudlery.com>

pkgname=s6
pkgver=2.13.2.0
pkgrel=1
pkgdesc='A small suite of programs for UNIX, designed to allow process supervision'
arch=('x86_64')
url="https://skarnet.org/software/${pkgname}"
license=('ISC')
depends=('skalibs' 'execline')
options=('!lto')
source=("${url}/${pkgname}-${pkgver}.tar.gz"
	"${pkgname}.patch")
sha256sums=('c5114b8042716bb70691406931acb0e2796d83b41cbfb5c8068dce7a02f99a45'
            '2d1f7b4f775ccd29a08ce8824a64e2a039ccef8b9682fa8c7761a1b206e276c1')

prepare() {
  patch -p0 -i ../${pkgname}.patch
}

build() {
  cd "${pkgname}-${pkgver}"

  ./configure --prefix=/usr --bindir=/usr/bin --sbindir=/usr/bin
  make
}

package() {
  cd "${pkgname}-${pkgver}"

  make DESTDIR="${pkgdir}" install
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
