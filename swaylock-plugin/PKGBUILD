# Maintainer: Manuel Stoeckl <com dоt mstoeckl аt wppkgb>
# SPDX-License-Identifier: 0BSD
pkgname=swaylock-plugin
pkgver=1.8.4
pkgrel=1
pkgdesc='A fork of the swaylock screen locker for Wayland supporting custom wallpaper drawing programs'
license=('MIT')
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64')
makedepends=('meson' 'ninja' 'scdoc' 'wayland-protocols')
depends=(
  'glibc' 'wayland' 'cairo' 'pam' 'libxkbcommon' 'systemd-libs' 'glib2'
  'gdk-pixbuf2' 'swaybg'
)
optdepends=(
  'mpvpaper: to implement video backgrounds'
  'windowtolayer: to use a terminal as background'
)
url="https://github.com/mstoeckl/swaylock-plugin"
source=("https://github.com/mstoeckl/swaylock-plugin/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=("49a6591ede8a906cd37e795d2f7f851c89081fd7cb2920ac5ddca459b7482610")
build() {
    arch-meson "$pkgname-$pkgver" build
    meson compile -C build
}
package() {
    meson install -C build --destdir "$pkgdir"
    install -Dm644 "$pkgname-$pkgver/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

