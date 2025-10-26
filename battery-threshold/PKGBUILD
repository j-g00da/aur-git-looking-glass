# Maintainer: Bennett Piater <bennett at piater dot name>
pkgname=battery-threshold
pkgver=1.1
pkgrel=1
pkgdesc="Systemd service to set battery charge thresholds"
arch=('any')
url="https://github.com/clawoflight/$pkgname"
license=('MIT')
depends=("bash")
source=(https://github.com/clawoflight/$pkgname/archive/refs/tags/v$pkgver.tar.gz)
sha256sums=('061c40f0b407cdd7a40456d7dea0858ff4d2f4381b3fadbdd30edb355f29954b')

package() {
    # Install the script
    install -Dm755 "$srcdir/$pkgname-$pkgver/battery-threshold.sh" "$pkgdir/usr/bin/battery-threshold.sh"

    # Install the systemd service
    install -Dm644 "$srcdir/$pkgname-$pkgver/battery-threshold.service" "$pkgdir/usr/lib/systemd/system/battery-threshold.service"
}
