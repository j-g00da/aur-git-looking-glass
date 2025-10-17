# Maintainer: Mario Blättermann <mario.blaettermann@gmail.com>
# Maintainer: Maud Spierings <maud_spierings@hotmail.com>

pkgname=glabels-qt-git
pkgver=r582.de85d47
pkgrel=1
pkgdesc="Development version of the next major version of gLabels (4.0)."
arch=('x86_64' 'aarch64')
url="https://github.com/j-evins/glabels-qt"
license=('GPL-3.0-only')
groups=()
depends=('qt6-base' 'qt6-svg' 'hicolor-icon-theme' 'glibc' 'gcc-libs' 'zlib' 'qrencode' 'zint')
makedepends=('qt6-tools' 'git' 'cmake' 'clang' 'qt6-declarative')
optdepends=()
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
replaces=()
backup=()
options=()
install=
source=('git+https://github.com/j-evins/glabels-qt.git')
noextract=()
md5sums=('SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "$srcdir/${pkgname%-git}"
	mkdir build
	cd build
	cmake -DCMAKE_INSTALL_PREFIX=/usr ..
	make
}

package() {
	cd "$srcdir/${pkgname%-git}"
	cd build
	make DESTDIR="$pkgdir/" install
}
