# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=play
pkgver=0.4.0
pkgrel=1
pkgdesc="TUI playground to experiment with programs such as grep, sed and awk"
arch=("x86_64")
url="https://github.com/paololazzari/play"
license=("Apache-2.0")
makedepends=("go")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=("7abe1745099e9b4d66e5fc62a1180f2170e8351953d0c6978dfc4719591cd00e")

build() {
    cd "$pkgname-$pkgver"
    go build
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 play "${pkgdir}/usr/bin/play"
    install -Dm 0644 LICENSE.md "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
}
