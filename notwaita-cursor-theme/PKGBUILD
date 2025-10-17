# Maintainer: Kiet "Shihotori" Huynh <11086238+superkidvn@users.noreply.github.com>
pkgname=notwaita-cursor-theme
pkgver=1.0.0_alpha1
pkgrel=1
pkgdesc="A cursor theme inspired by the Adwaita icons from the GNOME Project for Windows and Linux with HiDPI support."
arch=(any)
url="https://github.com/ful1e5/notwaita-cursor"
license=('LGPL-3.0-only')
source=(
  ${pkgname}-${pkgver//_/-}.tar.xz::"${url}/releases/download/v${pkgver//_/-}/Notwaita.tar.xz"
  COPYING_LGPL::"${url//github.com/raw.githubusercontent.com}/refs/heads/main/COPYING_LGPL"
)
sha256sums=('93928d9c64e2aa61e061efcfbdbf67ae15c458095c6d82f5ad790a1402d46cf2'
            'da7eabb7bafdf7d3ae5e9f223aa5bdc1eece45ac569dc21b3b037520b4464768')

package() {
  # Create directories
  install -d "${pkgdir}/usr/share/icons"

  # Install cursor themes
  cp -r "${srcdir}"/Notwaita-* "${pkgdir}/usr/share/icons"

  # Install license
  install -Dm0644 -t "${pkgdir}/usr/share/licenses/${pkgname}" "${srcdir}/COPYING_LGPL"
}
