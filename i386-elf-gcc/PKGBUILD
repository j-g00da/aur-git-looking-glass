# Maintainer: Dani Rodríguez <dani@danirod.es>
# Contributor: c0repwn3r <core@coredoes.dev>
pkgname=i386-elf-gcc
pkgver=15.2.0
pkgrel=1
epoch=
pkgdesc="GNU gcc for the i386- toolchain"
arch=(x86_64)
url="https://www.gnu.org/software/gcc"
license=('GPL')
groups=(i386-elf-toolchain)
makedepends=(gmp mpfr gcc)
depends=(xz libmpc i386-elf-binutils)
source=(
    "http://ftpmirror.gnu.org/gcc/gcc-$pkgver/gcc-$pkgver.tar.xz"
)
sha512sums=('89047a2e07bd9da265b507b516ed3635adb17491c7f4f67cf090f0bd5b3fc7f2ee6e4cc4008beef7ca884b6b71dffe2bb652b21f01a702e17b468cca2d10b2de')

build() {
    # GCC build fails with format-security.
    CFLAGS=${CFLAGS/-Werror=format-security/}
    CXXFLAGS=${CXXFLAGS/-Werror=format-security/}
    # Create temporary build dir
    mkdir -p "i386-gcc-$pkgver-build"
    cd "i386-gcc-$pkgver-build"
    # Configure, we are building in seperate directory to cleanly seperate the binaries from the source
    ../gcc-$pkgver/configure \
	--prefix=/usr \
	--target=i386-elf \
	--disable-nls \
	--disable-werror \
	--disable-multilib \
	--without-headers \
	--enable-languages=c,c++ \
	--disable-werror

    # Build
    make all-gcc
    make all-target-libgcc
}

check() {
    cd "i386-gcc-$pkgver-build"
    make -k check-gcc
}

package() {
    cd "i386-gcc-$pkgver-build"
    make install-gcc DESTDIR=$pkgdir
    make install-target-libgcc DESTDIR=$pkgdir
    # Remove conflicting files
    rm -rf $pkgdir/usr/share/info
    rm -rf $pkgdir/usr/share/man/man7
}
