# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=firefox-extension-singlefile-bin
pkgver=1.22.81
pkgrel=1
pkgdesc="Save an entire web page—including images and styling - as a single HTML file"
arch=("any")
url="https://addons.mozilla.org/addon/single-file/"
license=("MIT")
groups=("firefox-addons")
depends=("firefox>=126.0")
makedepends=("zip")
source=("$pkgname-$pkgver.xpi::https://addons.mozilla.org/firefox/downloads/file/4465739/single_file-$pkgver.xpi"
        "add-id.patch")
noextract=("$pkgname-$pkgver.xpi")
b2sums=("e577a3402396b071821449995805ab939c50f9c9ef3cb224ae9b1549b1cb0449dd498ae82833290448acc114b082645af402720bea60a5d4b1037f28c08e6da9"
        "56bb0272f682ae5bb73e8b658442acd2c4e54c0e7dcccf58b76a686c5995e4765d4bb4c5c4ac55e9a23d160e6f78e31d1516eca0eb5a921632b809ed74746c24")

prepare() {
    mkdir "$pkgname-$pkgver"
    bsdtar -xf "$pkgname-$pkgver.xpi" -C "$pkgname-$pkgver"
    cd "$pkgname-$pkgver"
    patch -p1 < "$srcdir/add-id.patch"
    zip -r "$pkgname-$pkgver.xpi" ./*
}

package() {
    cd $pkgname-$pkgver
    install -Dm 0644 "$pkgname-$pkgver.xpi" "$pkgdir/usr/lib/firefox/browser/extensions/addon@getsinglefile.com.xpi"
}
