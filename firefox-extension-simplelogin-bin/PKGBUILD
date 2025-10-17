# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=firefox-extension-simplelogin-bin
pkgver=3.0.7
pkgrel=1
pkgdesc="Create a different email for each website to hide your real email"
arch=("any")
url="https://github.com/simple-login/browser-extension"
license=("MIT")
groups=("firefox-addons")
depends=("firefox")
install="$pkgname.install"
source=("https://addons.mozilla.org/firefox/downloads/file/4458602/simplelogin-$pkgver.xpi")
b2sums=('1c7d764c4861f9673da2d5aea85ed1f10a676e6a095f3bb5ef8f5e904465bb89bd6460a7a601c01013e75bb3eec8293c8c8ce056fbaaf19a03a40130de0914c6')

package() {
    install -Dm 0644 simplelogin-$pkgver.xpi "$pkgdir/usr/lib/firefox/browser/extensions/addon@simplelogin.xpi"
}
