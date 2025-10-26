# Maintainer: Joao Costa <arch@joaocosta.dev>
pkgname=bambustudio-appimage
_pkgname=BambuStudio
pkgver=2.3.0
pkgrel=1
pkgdesc="PC Software for BambuLab and other 3D printers"
arch=('x86_64')
url="https://github.com/bambulab/BambuStudio"
license=('AGPL-3.0')
options=('!strip' '!debug')
provides=('bambustudio')
conflicts=('bambustudio' 'bambustudio-git' 'bambustudio-bin')
source=("${_pkgname}-${pkgver}.AppImage::https://github.com/bambulab/BambuStudio/releases/download/v02.03.00.70/Bambu_Studio_ubuntu-24.04_PR-8184.AppImage")
sha256sums=('60ef861e204e7d6da518619bd7b7c5ab2ae2a1bd9a5fb79d10b7c4495f73b172')

package() {
  cd "$srcdir"

  chmod +x "${_pkgname}-${pkgver}.AppImage"
  install -Dm755 "${_pkgname}-${pkgver}.AppImage" "$pkgdir/usr/bin/bambustudio"

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
