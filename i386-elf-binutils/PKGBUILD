# Maintainer: Dani Rodríguez <dani@danirod.es>
# Contributor: c0repwn3r <core@coredoes.dev>
pkgname=i386-elf-binutils
pkgver=2.45
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
sha256sums=(c50c0e7f9cb188980e2cc97e4537626b1672441815587f1eab69d2a1bfbef5d2)

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
