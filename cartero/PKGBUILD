# Maintainer: Dani Rodríguez <dani@danirod.es>
pkgname=cartero
pkgver=25.0
pkgrel=1
epoch=
pkgdesc="Make HTTP requests and test APIs"
arch=('x86_64')
url="https://github.com/danirod/cartero"
license=('GPL-3.0-or-later')
depends=('curl' 'glib2' 'gtk4' 'gtksourceview5' 'libadwaita' 'openssl')
makedepends=('blueprint-compiler' 'git' 'meson' 'rust')
conflicts=()
options=('!lto' '!strip')
source=("$pkgname-$pkgver.tar.xz::https://github.com/danirod/cartero/releases/download/v$pkgver/cartero-$pkgver.tar.xz")
sha256sums=('e5b60c652d6555f99862b15fb53c195588fa642362a90aa5b847cd427b45e452')

build() {
	# To disable client side decorations in your build (and enhance the
	# integration with desktop environments others than GNOME), add the
	# following flag at the end of the next command invocation:
	# -Ddecorations=no-csd
	arch-meson "${pkgname}-${pkgver}" build --wipe
	meson compile -C build
}

check() {
	meson test -C build --print-errorlogs || :
}

package() {
	meson install -C build --destdir "$pkgdir"
}
