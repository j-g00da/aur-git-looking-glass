# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=reddit-tui
pkgver=0.3.9
pkgrel=3
pkgdesc="Terminal UI for Reddit"
arch=("x86_64")
url="https://github.com/tonymajestro/reddit-tui"
license=("MIT")
makedepends=("go>=1.16")
conflicts=("reddit-tui")
provides=("reddit-tui")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('4f5dad492b776e67f9ed94fdc7bbcccabaa921ffdba7eb184619a830d05b5a33')

build() {
    cd "$pkgname-$pkgver"
    go build -o reddittui main.go
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 reddittui "${pkgdir}/usr/bin/reddittui"
    install -Dm 0644 LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"
    install -Dm 0644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
