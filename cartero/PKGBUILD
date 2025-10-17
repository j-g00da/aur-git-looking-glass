# Maintainer: Dani Rodríguez <dani@danirod.es>
pkgname=cartero
pkgver=0.2.4
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
sha256sums=('5da80922b7e921dd0e3ea1cce79ec2017efa9fb278eab1be3b3e3889db2421c5')

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
