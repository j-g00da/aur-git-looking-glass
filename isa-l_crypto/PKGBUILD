# Maintainer: fft
# Contributor: Roy Oursler <roy.j.oursler@intel.com>

pkgname=isa-l_crypto
pkgver=2.25.0
pkgrel=1
pkgdesc="A collection of optimized low-level functions targeting storage applications"
arch=(x86_64)
url="https://github.com/intel/${pkgname}"
license=('BSD-3-Clause')
makedepends=('nasm')
source=("${url}/archive/v${pkgver}.tar.gz")
b2sums=('18328b404a2686718fc8cf9bc596816e4521ec85440e8aad2bb40d32eabc606807617fc08c2790c4bb0a0b84648fa9820a4a6c19ac6a3cbbbc2cd96bddfd1eb9')

build() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    ./autogen.sh
    ./configure
    make
}

check() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    make check
    make tests
}

package() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    make install DESTDIR="${pkgdir}"
    install -Dm644 -t "${pkgdir}/usr/share/licenses/${pkgname}/" LICENSE
}
