# Maintainer: sos-developers <aur@saveoursecrets.com>
pkgname=saveoursecrets-bin
pkgver=2.0.1+125
pkgrel=1
pkgdesc="Secure password manager and wallet"
arch=('x86_64')
url="https://saveoursecrets.com"
license=('custom')
depends=(
  'glibc'
  'libsecret'
  'jsoncpp'
  'dbus'
)
source=("https://releases.saveoursecrets.com/beta/gui/${pkgver}/arch/x86_64/saveoursecrets.tgz")
sha256sums=('92e8d9b44d1e9f397fb03d78437c85fb46788ff8bc4b86b2f7476e5347f247ed')
# sha256sums=('SKIP')

package() {
  cd "$srcdir/saveoursecrets-${pkgver}"

  install -Dm755 saveoursecrets "$pkgdir/usr/opt/saveoursecrets/saveoursecrets"
  install -Dm755 sos-extension-helper "$pkgdir/usr/opt/saveoursecrets/sos-extension-helper"
  cp -r lib "$pkgdir/usr/opt/saveoursecrets/"
  cp -r data "$pkgdir/usr/opt/saveoursecrets/"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/saveoursecrets"

  install -d "$pkgdir/usr/bin"
  ln -sr "$pkgdir/usr/opt/saveoursecrets/saveoursecrets" "$pkgdir/usr/bin/saveoursecrets"
  ln -sr "$pkgdir/usr/opt/saveoursecrets/sos-extension-helper" "$pkgdir/usr/bin/sos-extension-helper"
}
