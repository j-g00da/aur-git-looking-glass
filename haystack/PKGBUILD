pkgname=haystack
pkgver=0.4.0
pkgrel=1
pkgdesc="A tool to categorise your screenshots"
arch=('x86_64' 'aarch64')
url="https://github.com/JohnCosta27/haystack-arch"
license=('MIT')
depends=('cairo' 'desktop-file-utils' 'gdk-pixbuf2' 'glib2' 'gtk3' 'hicolor-icon-theme' 'libsoup' 'pango' 'webkit2gtk-4.1' 'slurp' 'grim')
options=('!strip' '!emptydirs')
install=${pkgname}.install
source_x86_64=("${url}/releases/download/v${pkgver}/Haystack_${pkgver}_amd64.deb")
sha256sums_x86_64=('5065ab26cd732d20153067f5d02e9f03137c68a42d37cbd865a13727b6181c3d')

package() {
  # Extract package data
  tar -xvf data.tar.gz -C "${pkgdir}"
}
