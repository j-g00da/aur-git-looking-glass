# Maintainer: Vaishakh G K <vaishakhgk2006@gmail.com>
pkgname='systune-git'
pkgver=r48.58d6da0
pkgrel=2
pkgdesc="A lightweight and efficient GTK-based system settings manager"
arch=('x86_64')
url="https://github.com/fulgurcode/systune"
license=('GPL-3.0-or-later')
depends=('gtk4' 'libadwaita' 'glibc' 'grep' 'sed' 'awk')
makedepends=('git' 'make')
optdepends=(
	'libpulse: For audio controls'
	'xorg-xrandr: To change display resolution in Xorg'
	'wlr-randr: To change display resolution in wlroots-based Wayland compositors'
	'swww: To set background in Wayland'
	'feh: To set background in Xorg'
	'brightnessctl: For brightness control'
	'bluez: For Bluetooth controls'
	'networkmanager: For WiFi connections'
	'polkit: Required for superuser permissions in firewall and security settings'
	'ufw: For firewall management'
)
source=("$pkgname::git+https://github.com/FulgurCode/systune.git")
sha256sums=('SKIP')

pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

build() {
	cd "$pkgname"
	make all
}

package() {
	cd "$pkgname"
  install -Dm755 "./bin/systune" "$pkgdir/usr/bin/systune"
  install -Dm755 "./systune.desktop" "$pkgdir/usr/share/applications/systune.desktop"
  install -Dm644 "./README.md" "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 "./assets/systune.png" "$pkgdir/usr/share/pixmaps/systune.png"

  mkdir "$pkgdir/usr/share/systune"
	cp -r "./ui/" "$pkgdir/usr/share/systune/ui/"
	cp -r "./styles/" "$pkgdir/usr/share/systune/styles/"
}
