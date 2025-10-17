# Maintainer: Bouteiller a2n Alan <a2n.dev@pm.me>
pkgname=postier-bin
pkgver=1.5.0
pkgrel=2
pkgdesc="Fully free & open-source API client"
arch=('x86_64')
url="https://github.com/bouteillerAlan/postier"
license=('GPL')
depends=('cairo' 'desktop-file-utils' 'gdk-pixbuf2' 'glib2' 'gtk3' 'hicolor-icon-theme' 'libsoup3' 'pango' 'webkit2gtk-4.1')
options=('!strip' '!emptydirs')
install=${pkgname}.install
source_x86_64=("${url}/releases/download/v"${pkgver}"/Postier_"${pkgver}"_amd64.deb")
sha256sums_x86_64=('16309a68bda424e4e2ac9081344e5dd73d5bb976cb0b912e75b98fb2239bfb88')
package() {
  # Extract package data
  tar -xz -f data.tar.gz -C "${pkgdir}"
}
