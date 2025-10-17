# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=firefox-extension-skip-redirect-bin
pkgver=2.3.6
pkgrel=1
pkgdesc="Skip intermediary pages that some pages use before redirecting to a final page"
arch=("any")
url="https://github.com/sblask-webextensions/webextension-skip-redirect"
license=("MIT")
groups=("firefox-addons")
depends=("firefox")
conflicts=("firefox-extension-skip-redirect")
source=("https://addons.mozilla.org/firefox/downloads/file/3920533/skip_redirect-$pkgver.xpi")
sha256sums=("dbe8950245c1f475c5c1c6daab89c79b83ba4680621c91e80f15be7b09b618ae")

package() {
    install -Dm 0644 skip_redirect-$pkgver.xpi "$pkgdir/usr/lib/firefox/browser/extensions/skipredirect@sblask.xpi"
}
