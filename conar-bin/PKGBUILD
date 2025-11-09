# Maintainer: Bouteiller a2n Alan <hi@a2n.dev>
pkgname=conar-bin
pkgver=0.23.0
pkgrel=1
pkgdesc="AI-powered tool for working with Postgres."
arch=('x86_64')
url="https://github.com/wannabespace/conar"
license=('AGPL-3.0-or-later')
depends=(
  'gcc-libs'
  'alsa-lib'
  'libxfixes'
  'libx11'
  'glib2'
  'libxkbcommon'
  'libxcb'
  'glibc'
  'nss'
  'libxrandr'
  'libxcomposite'
  'libcups'
  'mesa'
  'pango'
  'gtk3'
  'systemd-libs'
  'nspr'
  'cairo'
  'expat'
  'at-spi2-core'
  'libxdamage'
  'libxext'
  'dbus'
  'hicolor-icon-theme'
)
options=('!strip' '!emptydirs')
source_x86_64=("${url}/releases/download/v"${pkgver}"/Conar-Linux-"${pkgver}".deb")
sha256sums_x86_64=('07cdcf27c9a765440fa5718a5fd842533020e48ab5e960275db5d118dd483bb8')
package() {
  # Extract the .deb file
  ar -x "${srcdir}/Conar-Linux-${pkgver}.deb"

  # Extract the data archive
  tar -xJ -f data.tar.xz -C "${pkgdir}"

  # Create symlink for command line usage
  install -dm755 "${pkgdir}/usr/bin"
  ln -s "/opt/Conar/Conar" "${pkgdir}/usr/bin/conar"

  # Fix desktop file path if it exists
  if [ -f "${pkgdir}/usr/share/applications/conar.desktop" ]; then
    sed -i 's|/opt/Conar/Conar|conar|g' "${pkgdir}/usr/share/applications/conar.desktop"
  fi
}

