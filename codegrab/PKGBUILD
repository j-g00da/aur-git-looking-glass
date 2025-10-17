# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=codegrab
pkgver=1.0.7
pkgrel=1
pkgdesc="CLI and TUI for selecting and bundling code into a single, LLM-ready output file"
arch=("x86_64")
url="https://github.com/epilande/codegrab"
license=("MIT")
makedepends=("go")
provides=("codegrab")
conflicts=("codegrab")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
b2sums=('8d8b5a834e0e5544464f1a1281cb3afd639d204adb01899a930af36fba62d872d270713ee4e416237ca9cd8cfcf182450ddcd0046859e8a15bbc5f709cf7908f')

build() {
    cd "$pkgname-$pkgver"
    go build ./cmd/grab
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 755 grab "$pkgdir/usr/bin/grab"
    install -Dm 644 LICENSE "$pkgdir/usr/share/licences/$pkgname/LICENSE"
    install -Dm 644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}
