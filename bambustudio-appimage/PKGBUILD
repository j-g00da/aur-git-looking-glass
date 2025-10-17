# Maintainer: Joao Costa <arch@joaocosta.dev>
pkgname=bambustudio-appimage
_pkgname=BambuStudio
pkgver=2.2.2
pkgrel=3
pkgdesc="PC Software for BambuLab and other 3D printers"
arch=('x86_64')
url="https://github.com/bambulab/BambuStudio"
license=('AGPL-3.0')
options=('!strip' '!debug')
provides=('bambustudio')
conflicts=('bambustudio' 'bambustudio-git' 'bambustudio-bin')
source=("${_pkgname}-${pkgver}.AppImage::https://github.com/bambulab/BambuStudio/releases/download/v02.02.02.56/Bambu_Studio_ubuntu-24.04_PR-8184.AppImage"
  "LICENSE")
sha256sums=('ce28a910ccf9f251bffaec6e6c2779ddce818c9f56ddda09f7f67c549a7e65ae'
  '57c8ff33c9c0cfc3ef00e650a1cc910d7ee479a8bc509f6c9209a7c2a11399d6')

package() {
  cd "$srcdir"

  chmod +x "${_pkgname}-${pkgver}.AppImage"
  install -Dm755 "${_pkgname}-${pkgver}.AppImage" "$pkgdir/usr/bin/bambustudio"
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  ./"${_pkgname}-${pkgver}.AppImage" --appimage-extract &>/dev/null

  if [ -f "squashfs-root/BambuStudio.png" ]; then
    install -Dm644 "squashfs-root/BambuStudio.png" "$pkgdir/usr/share/pixmaps/BambuStudio.png"
  else
    msg2 "Warning: Could not automatically find an icon file (BambuStudio.png) within the AppImage."
    msg2 "         Desktop entry icon might be missing."
  fi

  if [ -f "squashfs-root/BambuStudio.desktop" ]; then
    sed -i 's|Exec=AppRun|Exec=/usr/bin/bambustudio|' "squashfs-root/BambuStudio.desktop"
    install -Dm644 "squashfs-root/BambuStudio.desktop" "$pkgdir/usr/share/applications/BambuStudio.desktop"
  else
    msg2 "Fail: Could not automatically find desktop icon file (BambuStudio.desktop) within the AppImage."
    exit 1
  fi
}
