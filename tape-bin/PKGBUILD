# Maintainer: Bouteiller a2n Alan <a2n.dev@pm.me>
pkgname=tape-bin
appname=tape
pkgver=3.2.4
pkgrel=2
pkgdesc="Take notes without bloat"
arch=('x86_64')
url="https://github.com/results-may-vary-org/tape"
license=('GPL')
depends=('glibc' 'gtk3' 'webkit2gtk-4.1' 'desktop-file-utils' 'hicolor-icon-theme')
options=('!strip' '!emptydirs')
install=${pkgname}.install
source_x86_64=("${url}/releases/download/v"${pkgver}"/"${appname}"_"${pkgver}"_amd64.deb")
sha256sums_x86_64=('0728b1e1ffc576d9bbf46e6537f607ece60e5e011def5d1d2daf0637c5485b8d')
package() {
  # Extract the deb package
  ar x "${appname}_${pkgver}_amd64.deb"

  # Extract package data
  tar -xz -f data.tar.gz -C "${pkgdir}"

  # Fix permissions
  chmod 755 "${pkgdir}/usr/bin/tape"
}
