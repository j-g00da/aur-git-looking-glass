# Maintainer: Kayque Pereira <kayquesousa02004@gmail.com>
# Contributor: David Marrero <bdface[at]proton[dot]me>
# Contributor: Mattia Borda <mattiagiovanni.borda@icloud.com>

pkgname=gnome-shell-extension-hanabi-git
pkgver=r271.4bd29ce
pkgrel=1
pkgdesc='Live Wallpaper for GNOME'
arch=(any)
url=https://github.com/jeffshee/gnome-ext-hanabi
license=(GPL3)
makedepends=(meson)
depends=(
        'gnome-shell'
        'gjs'
        'gst-plugins-bad'
        'gst-plugins-base'
        'gst-plugins-good'
        'gstreamer'
        'gtk4'
        'libadwaita'
)
optdepends=(
        'clapper: Hanabi can use clappersink for the best performance'
        'gst-plugin-va: experimental performance improvement for Intel/AMD Wayland users'
        'gst-libav: required to play mp4 files, among others'
        'gstreamer-vaapi: Video acceleration for Intel/AMD users'
)
source=(git+$url)
b2sums=(SKIP)

pkgver() {
	cd gnome-ext-hanabi
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	arch-meson gnome-ext-hanabi build
}

package() {
	DESTDIR="$pkgdir" meson install -C build
}
