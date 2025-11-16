# Maintainer: Dani Rodríguez <dani@danirod.es>
# Contributor: c0repwn3r <core@coredoes.dev>
pkgname=i386-elf-binutils
pkgver=2.45.1
pkgrel=1
epoch=
pkgdesc="GNU binutils for the i386- toolchain"
arch=(x86_64)
url="https://www.gnu.org/software/binutils"
license=('GPL')
groups=(i386-elf-toolchain)
makedepends=(gcc)
depends=(xz)
source=("http://ftpmirror.gnu.org/binutils/binutils-$pkgver.tar.xz")
sha256sums=("5fe101e6fe9d18fdec95962d81ed670fdee5f37e3f48f0bef87bddf862513aa5")

build() {
    # Create temporary build dir
    mkdir -p "i386-binutils-$pkgver-build"
    cd "i386-binutils-$pkgver-build"

    # Configure, we are building in seperate directory to cleanly seperate the binaries from the source
    ../binutils-$pkgver/configure --prefix=/usr --target=i386-elf --disable-nls --disable-werror --disable-multilib --enable-interwork

    # Build
    make
}

check() {
    cd "i386-binutils-$pkgver-build"

    # unset LDFLAGS as testsuite makes assumptions about which ones are active
    # ignore failures in gold testsuite...
    make -k LDFLAGS="" check
}

package() {
    cd "i386-binutils-$pkgver-build"
    make install DESTDIR=$pkgdir
    # Remove conflicting files
    rm -rf $pkgdir/usr/share/info
    rm -rf $pkgdir/usr/lib/bfd-plugins
}
