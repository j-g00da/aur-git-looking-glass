# Maintainer: Noah Witt <noah@noah-witt.com>

pkgname=charge-threshold
pkgver=1.0.1
pkgrel=1
pkgdesc="A simple script to set the battery charge threshold on Linux systems."
arch=('any')
url="https://github.com/noah-witt/charge-threshold" # Replace with your actual repo
license=('MIT') # Or a more appropriate license for your script
depends=('bash') # No specific dependencies for this script

source=("charge-threshold")
sha256sums=('SKIP') # Replace with the actual SHA256 sum of your script

package() {
  install -D -m755 "${srcdir}/charge-threshold" "${pkgdir}/usr/bin/charge-threshold"
}
