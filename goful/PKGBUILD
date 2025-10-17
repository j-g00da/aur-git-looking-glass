# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=goful
pkgver=0.2.1
pkgrel=1
pkgdesc="CUI file manager written in Go"
arch=("x86_64" "i686" "aarch64")
url="https://github.com/anmitsu/goful"
license=("MIT")
makedepends=("go")
provides=("goful")
conflicts=("goful-bin" "goful")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
b2sums=("3633920f46b8c18b8944de785c6ccb4e201e29bb76a73bef27e2bdfbfd73634e17b54f8d0b1da18bfc925c5e9f49dfb169e768186d931bdde5fda9427415ab14")

build() {
    cd "$pkgname-$pkgver"
    go build -o goful
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 goful "$pkgdir/usr/bin/goful"
    install -Dm 0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
