# Maintainer: stag-enterprises < x [at] stag [dot] lol >

pkgname=alden
pkgver=0.2
pkgrel=1
pkgdesc="Detachable terminal sessions without breaking scrollback"
arch=("x86_64" "aarch64")
depends=("base-devel")
url="https://ansuz.sooke.bc.ca/entry/389"
license=("GPL-3.0-only")
changelog="CHANGELOG"
source=("https://files.northcoastsynthesis.com/alden-$pkgver.tar.gz")
sha256sums=('6ba8e069ea509c320e4c84a6d2ba9d0091b34338cf7204be3e944178dd2c8e2f')
sha512sums=('ffc2e796c5484120e31517b0410b81cf4841fbacb4b141890e80b5f50491aa8949c7d9d382a59d10a8fa547a06541ac339b643adc93e8dbd61d3977fe2dd8445')
b2sums=('e6d48e4542638ab3e8a09d5712e4df279b04b6a3607e955c604d009ac8f02afe833b855401885b5f40e34cafb0deeca5083dc26a63db5ee4f3f0616a5261f838')

build() {
     cd "$srcdir/alden-$pkgver"
     ./configure --prefix=/usr
     make
}

check() {
     cd "$srcdir/alden-$pkgver"
     make check
}

package() {
     cd "$srcdir/alden-$pkgver"
     make DESTDIR="$pkgdir/" install
}
