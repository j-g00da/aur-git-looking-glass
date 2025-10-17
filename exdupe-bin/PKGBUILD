# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=exdupe
pkgname=$_projectname-bin
pkgver=3.0.0
pkgrel=1
arch=("x86_64")
pkgdesc="Fast file archiver that supports data deduplication and differential backups"
url="https://github.com/rrrlasse/$_projectname"
license=("unknown")
source=("$pkgname-$pkgver.tar.gz::$url/releases/download/v${pkgver}/${_projectname}_${pkgver}_linux_amd64.tar.gz")
b2sums=('fbcef07df7da68be33be63d1f7bdb42b36c217f5ce3adae80ccc87c7528e7cf5da02d1d0f2e12adc106ecfe0429e3a622a7892cd974199983c3cbed7590e6bff')

package() {
    install -Dm 0755 exdupe "$pkgdir/usr/bin/exdupe"
}
