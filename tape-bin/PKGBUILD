# Maintainer: Bouteiller a2n Alan <a2n.dev@pm.me>
pkgname=tape-bin
appname=tape
pkgver=3.3.0
pkgrel=2
pkgdesc="Take notes without bloat"
arch=('x86_64')
url="https://github.com/results-may-vary-org/tape"
license=('GPL')
depends=('glibc' 'gtk3' 'webkit2gtk-4.1' 'desktop-file-utils' 'hicolor-icon-theme')
options=('!strip' '!emptydirs')
install=${pkgname}.install
source_x86_64=("${url}/releases/download/v"${pkgver}"/"${appname}"_"${pkgver}"_amd64.deb")
sha256sums_x86_64=('5f196a740ea436c8e78c1e996c6ff01218600a322f4911ece2bad37477fd1131')
package() {
  # Extract the deb package
  ar x "${appname}_${pkgver}_amd64.deb"

  # Extract package data
  tar -xz -f data.tar.gz -C "${pkgdir}"

  # Fix permissions
  chmod 755 "${pkgdir}/usr/bin/tape"
}
