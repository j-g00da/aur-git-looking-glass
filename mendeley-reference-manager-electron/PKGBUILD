# Maintainer: Supernovatux <thulashitharan.d at gmail dot com>
_electron=electron
_pkgname='mendeley-reference-manager'
pkgname=${_pkgname}-electron
pkgver=2.130.2
pkgrel=1
pkgdesc="Mendeley Reference Manager using system provided ${_electron} for increased security and performance"
arch=('x86_64')
provides=("${_pkgname}")
conflicts=("${_pkgname}")
depends=("${_electron}" 'harfbuzz' 'libgl' 'libxss')
url='https://www.mendeley.com/download-reference-manager'
license=('custom')

_file=${_pkgname}-${pkgver}-x86_64.AppImage
source=(https://static.mendeley.com/bin/desktop/${_file})
sha256sums=('1cb514a16fa3d16f62106bb422b6ddff2ed5823dab0864fbb4318cce6321dea2')

options=('!strip')

prepare() {
  # Some parts taken from the orginal mendeley-reference-manager package
  # Extract AppImage contents so we install bypassing every and all AppImage
  # desktop integration/deployment mechanisms
  chmod +x "${_file}"
  "./${_file}" --appimage-extract &>/dev/null
}

package() {
  install -d "$pkgdir"/usr/bin/
  install -d "$pkgdir"/usr/lib/${_pkgname}/
  install -d "$pkgdir"/usr/share/applications/
  install -d "$pkgdir"/usr/share/icons/
  echo '#!/bin/sh' >> "$pkgdir"/usr/bin/${_pkgname}
  echo "exec electron /usr/lib/${_pkgname}/app.asar \"\$@\"" >> "$pkgdir"/usr/bin/${_pkgname}
  chmod +x ${pkgdir}/usr/bin/${_pkgname}
  
  install -m644 squashfs-root/mendeley-reference-manager.png "$pkgdir"/usr/share/icons/

  sed -i "s%Exec=AppRun%Exec=/usr/bin/${_pkgname}%g" squashfs-root/mendeley-reference-manager.desktop
  install -m644 squashfs-root/mendeley-reference-manager.desktop "$pkgdir"/usr/share/applications/
  install -m644 squashfs-root/resources/app.asar "$pkgdir"/usr/lib/${_pkgname}/
}

