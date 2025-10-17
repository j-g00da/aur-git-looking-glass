# Maintainer: Kartik Jain <kartik@yeezus.live>
pkgname=deja-file
pkgver=1.0
pkgrel=1
pkgdesc="CLI tool to detect and delete duplicate files by MD5 hash"
arch=('x86_64')
url="https://github.com/KartikJain14/deja-file"
license=('MIT')
depends=('openssl')
source=("git+$url")
sha256sums=('SKIP')

build() {
    cd "$srcdir/$pkgname"
    g++ -std=c++17 -o deja-file deja-file.cpp -lssl -lcrypto
}

package() {
    install -Dm755 "$srcdir/$pkgname/deja-file" "$pkgdir/usr/bin/deja-file"
}
