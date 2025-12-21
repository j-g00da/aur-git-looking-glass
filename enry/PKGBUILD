# Maintainer: Hugo ARNAL <aur at hugoarnal dot com>

pkgname=enry
pkgver=1.3.0
pkgrel=2
pkgdesc="A command-line tool based on enry"
url="https://github.com/go-enry/enry/"
license=("Apache-2.0")
arch=("x86_64")
makedepends=("go")
checkdepends=("go")
provides=("$pkgname")
source=("https://github.com/go-enry/enry/archive/v$pkgver.tar.gz")
sha256sums=("39058e160b27828eceadaf374bfb380434acdcf8857da4a0b3e3600c1d136cac")

build() {
	cd "$srcdir/$pkgname-$pkgver"
    go build
}

package() {
	cd "$srcdir/$pkgname-$pkgver"
    install -Dm755 enry "$pkgdir/usr/bin/enry"
}

check() {
	cd "$srcdir/$pkgname-$pkgver"
    go test
}
