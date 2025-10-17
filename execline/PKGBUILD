# Maintainer:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: Marcin (CTRL) Wieczorek <marcin@marcin.co>
# Contributor: Josh VanderLinden <arch@cloudlery.com>

pkgname=execline
pkgver=2.9.7.0
pkgrel=1
pkgdesc='A (non-interactive) scripting language, like sh'
arch=('x86_64')
url="https://skarnet.org/software/${pkgname}"
license=('ISC')
depends=('skalibs')
options=('!lto' '!debug')
source=("${url}/${pkgname}-${pkgver}.tar.gz"
	"${pkgname}.patch")
sha256sums=('73c9160efc994078d8ea5480f9161bfd1b3cf0b61f7faab704ab1898517d0207'
            '3a4d2fd664921d484a0ceb5a76533a09adbb0ca03a46b456d0840fe92e320523')

prepare() {
  patch -p0 -i ../${pkgname}.patch
}

build() {
  cd "${pkgname}-${pkgver}"

  ./configure --prefix=/usr --libdir=/usr/lib
  make
}

package() {
  cd "${pkgname}-${pkgver}"

  make DESTDIR="${pkgdir}" install
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
