# Maintainer: Supernovatux <thulashitharan.d at gmail dot com>
pkgname=xdg-desktop-portal-gtk4-git
pkgver=r1.0551064
pkgrel=1
pkgdesc="GTK4 implementation of xdg-desktop-portal "
arch=('x86_64')
url="https://github.com/mahkoh/xdg-desktop-portal-gtk4"
license=('LGPL')
depends=('xdg-desktop-portal')
makedepends=('meson' 'git' 'cargo')
provides=('xdg-desktop-portal-impl' 'xdg-desktop-portal-gtk4')
conflicts=('xdg-desktop-portal-gtk4')
source=("git+${url}.git")
sha256sums=('SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "$srcdir/${pkgname%-git}"
	export RUSTUP_TOOLCHAIN=stable
	cargo fetch --locked --target "$(rustc -vV | sed -n 's|host: ||p')"
}

build() {
	cd "$srcdir/${pkgname%-git}"
	export RUSTUP_TOOLCHAIN=stable
	cargo build --release --frozen
	meson setup build -Dprefix=/usr
}

package() {
	cd "$srcdir/${pkgname%-git}"
	DESTDIR="${pkgdir}" meson install -C build
}
