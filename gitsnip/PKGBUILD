# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=gitsnip
pkgver=0.1.1
pkgrel=1
arch=("x86_64")
pkgdesc="CLI tool to download specific directories from a git repository"
url="https://github.com/dagimg-dot/gitsnip"
license=("MIT")
makedepends=("go")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
b2sums=("53c641b89941bcc253976a4a7cb682a9b7c075753332eb2babbfae8e78517af0187e6cb41b4e9b6037a5abc3353e7b7268a1da4f711632b3ca9b3232cc85c336")

build() {
    cd "$pkgname-$pkgver"
    make
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 bin/gitsnip "$pkgdir/usr/bin/gitsnip"
    install -Dm 0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
