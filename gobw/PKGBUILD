# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=gobw
pkgver=1.0
pkgrel=2
pkgdesc="Bitwarden TUI written in Go"
arch=("x86_64")
url="https://github.com/007Psycho007/gobw"
license=("GPL-3.0-only")
depends=("bitwarden-cli")
makedepends=("go")
conflicts=("gobw")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('085fd99aaa58b929b66b7d07d50b12cacc4125437954446cd365cdf3de8ce0b0')

build() {
    cd "$pkgname-$pkgver"
    go build
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 gobw "${pkgdir}/usr/bin/gobw"
    install -Dm 0644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm 0644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
