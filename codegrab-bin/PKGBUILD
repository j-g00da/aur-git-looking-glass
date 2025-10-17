# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=codegrab
pkgname=$_projectname-bin
pkgver=1.0.7
pkgrel=1
pkgdesc="CLI and TUI for selecting and bundling code into a single, LLM-ready output file"
arch=("x86_64")
url="https://github.com/epilande/codegrab"
license=("MIT")
provides=("codegrab")
conflicts=("codegrab")
source=("$pkgname-$pkgver.tar.gz::$url/releases/download/v$pkgver/${_projectname}_${pkgver}_Linux_x86_64.tar.gz")
b2sums=('2e67d991fb4956fcf71502d6751aa6021c6b095933f0f6e296b4d6c8691a62de6587392e59896471b0964ba1fc81f52f7e6619de4e82c5585a8a78b8c6a31b6c')

package() {
    install -Dm 755 grab "$pkgdir/usr/bin/grab"
    install -Dm 644 LICENSE "$pkgdir/usr/share/licences/$pkgname/LICENSE"
    install -Dm 644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}
