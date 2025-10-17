# Maintainer: fk29g <fk29g.uphill912@slmails.com>
# Maintainer: giorgiopapini <papini.computing746@slmail.me>
pkgname=netdump
pkgver=1.0.1
pkgrel=1
pkgdesc="Network packet analyzer supporting real-time and offline analysis with ASCII visualization"
arch=("x86_64")
url="https://github.com/giorgiopapini/netdump"
license=("GPL-3.0-only")
depends=("libpcap")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('050b225a198478ef99506ef308e0b327912566546bef70081cc1ef368eebdfdc')
_PREFIX=/usr
_LIBDIR="${_PREFIX}/lib"

build() {
    cd "$pkgname-$pkgver"
    LIBDIR="$LIBDIR" make
}

package() {
    cd "$pkgname-$pkgver"
    mkdir -p "${pkgdir}${_PREFIX}/bin"
    mkdir "${pkgdir}${_PREFIX}/lib"
    make PREFIX="$_PREFIX" DESTDIR="$pkgdir" LIBDIR="$_LIBDIR" install
    install -Dm 0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
