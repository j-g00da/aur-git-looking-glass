# Maintainer: Jorge F. Sanchez <mail@jfsanchez.net>
pkgname=firefox-profile-launcher
pkgver=1.0
pkgrel=2
pkgdesc="Simple Firefox profile launcher"
arch=("any")
url="https://github.com/jfsanchez91/firefox-profile-launcher"
license=("MIT")
depends=("gtk4" "python-gobject" "python3" "firefox")
source=(
    "firefox-profile-launcher"
    "firefox-profile-launcher.desktop"
    "style.css"
)
sha256sums=("SKIP" "SKIP" "SKIP")

package() {
    install -Dm755 "$srcdir/firefox-profile-launcher" "$pkgdir/usr/bin/firefox-profile-launcher"
    install -Dm644 "$srcdir/style.css" "$pkgdir/usr/share/firefox-profile-launcher/style.css"
    install -Dm644 "$srcdir/firefox-profile-launcher.desktop" "$pkgdir/usr/share/applications/firefox-profile-launcher.desktop"
}
