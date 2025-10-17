# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=gitnapped
pkgver=0.1.4
pkgrel=3
pkgdesc="Find out why you didn’t sleep"
arch=("x86_64")
url="https://github.com/Solexma/gitnapped"
license=("AGPL-3.0-only")
makedepends=("rust")
provides=("gitnapped")
conflicts=("gitnapped")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=("31a459cd6554d597335727a921161c8142868611f2acbfb5787fe60b77fee7e1")

build() {
    cd "$pkgname-$pkgver"
    cargo build --release
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 target/release/gitnapped "$pkgdir/usr/bin/gitnapped"
    install -Dm 0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm 0644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}
