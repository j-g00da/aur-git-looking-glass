# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Noah Heller <softwareenginer at pm dot me>
pkgname=advantagescope
pkgver=4.1.6
pkgrel=1
epoch=
pkgdesc="robot diagnostics, log review/analysis, and data visualization application tool"

arch=(x86_64)
url="https://github.com/Mechanical-Advantage/AdvantageScope/releases/download/v${pkgver}/advantagescope-linux-x64-v${pkgver}.pacman"
license=('MIT')
groups=()
depends=(nspr libxdamage dbus nss libxcb libxext glib2 libxrandr mesa libxfixes alsa-lib alsa-lib glibc gcc-libs libcups libxkbcommon cairo at-spi2-core pango expat libx11 gtk3 libdrm libxcomposite hicolor-icon-theme)
makedepends=(curl tar)
checkdepends=()
optdepends=()
provides=(libEGL.so libGLESv2.so libffmpeg.so libvk_swiftshader.so libvulkan.so)
conflicts=(advantagescope-git)
replaces=()
backup=()
options=()
install=
changelog=
source=("$url")
noextract=()
sha256sums=('SKIP')
validpgpkeys=()

build() {
  tar xvf $pkgname-linux-x64-v$pkgver.pacman
  curl -OL https://raw.githubusercontent.com/Mechanical-Advantage/AdvantageScope/refs/heads/main/LICENSE
}
package() {
  cp -rf opt "$pkgdir"
  cp -rf usr "$pkgdir"
  mkdir -p "$pkgdir/usr/bin"
  ln -s "/opt/AdvantageScope/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/$pkgname/LICENSE"

}
