# Contributor: Philippe Hürlimann <p@hurlimann.org>
# Contributor: Michel Zou <xantares09@hotmail.com>
# Maintainer: Kuan-Yen Chou <kuanyenchou at gmail dot com>

pkgname=retdec
pkgver=5.0
pkgrel=3
pkgdesc="A retargetable machine-code decompiler based on LLVM"
arch=('x86_64')
url="https://github.com/avast/retdec"
license=('MIT')
depends=('openssl' 'python' 'zlib')
makedepends=('cmake3' 'doxygen' 'graphviz')
optdepends=('upx: To use UPX unpacker in the preprocessing stage'
            'graphviz: To generate call or control flow grpahs')
source=("https://github.com/avast/${pkgname}/archive/refs/tags/v${pkgver}.tar.gz"
        '00-fix-missing-cstdint.patch'
        '01-use-yaramod-v3.21.0.patch')
sha256sums=('216dc62fd54ff06277497492dbf44bc7a91e39249d8aefdee2e4f10fc903ce85'
            '336c3eaf70faf398adbc4a5253278f89913b22f551882b802f857f1f41a441c0'
            'd461f420b23fe00669c24c82d94de97b8caffde84ad164ed47f19e77348c55e3')

prepare() {
    cd "$srcdir/$pkgname-$pkgver"
    patch -Np1 -i "$srcdir/00-fix-missing-cstdint.patch"
    patch -Np1 -i "$srcdir/01-use-yaramod-v3.21.0.patch"
}

build() {
    cd "$srcdir/$pkgname-$pkgver"
    # The use of cmake3 is needed for now because CMake 4.0 has removed
    # compatibility with CMake < 3.5, which leads to configuration errors with
    # llvm, yaramod, and fmt. We may consider switching back to cmake when
    # retdec creates a new release that compiles with the updated version.
    cmake3 -B build -S . \
        -DCMAKE_INSTALL_PREFIX="$pkgdir/usr" \
        -DCMAKE_BUILD_TYPE=Release \
        -DRETDEC_DOC=ON
    cmake3 --build build
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    cmake3 --install build
    install -Dm 644 -t "${pkgdir}/usr/share/licenses/${pkgname}" LICENSE*
}

# vim: set sw=4 ts=4 et:
