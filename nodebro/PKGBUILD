# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=nodebro
pkgver=0.3.0
pkgrel=1
pkgdesc="TUI to track git tag releases on github"
arch=("x86_64")
url="https://github.com/jonaburg/nodebro"
license=("GPL-3.0-only")
makedepends=("go")
install="nodebro.install"
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=("ff8cd7fac004122e68502d16bb89d9ce2a3382eb49b39ad8988873586a55dbb8")

build() {
    cd "$pkgname-$pkgver"
    go build -o nodebro
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 nodebro "${pkgdir}/usr/bin/nodebro"
    install -Dm 0644 example.config.toml "${pkgdir}/etc/${pkgname}/example.config.toml"
    install -Dm 0644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
