# Maintainer: Yurii Kolesnykov <root@yurikoles.com>
# Contributor: Solomon Choina <shlomochoina@gmail.com>
#
# Pull Requests are welcome here: https://github.com/yurikoles-aur/kcm-grub2-git
#

pkgname=kcm-grub2-git
pkgver=0.6.4.r301.g1281187
pkgrel=2
pkgdesc="A KDE Control Module for configuring the GRUB2 bootloader"
arch=('x86_64')
url='https://invent.kde.org/system/kcm-grub2'
license=('GPL-3.0-or-later')
depends=(
	'grub'
	'hwinfo'
	'kcmutils'
	'libmagick'
)
makedepends=(
	'cmake'
	'extra-cmake-modules'
	'git'
)
conflicts=('grub2-editor-frameworks')
provides=('grub2-editor-frameworks')
optdepends=(
	'os-prober: To detect other OSes when generating grub.cfg in BIOS systems'
)
source=("${pkgname}::git+${url}.git")
sha256sums=('SKIP')

pkgver() {
	# cutting off 'v' prefix that presents in the git tag
	git -C "${pkgname}" describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	cmake \
		-B build \
		-S "${pkgname}" \
		-Wno-dev
	cmake --build build
}

# No tests were found!!
check() {
	ctest --test-dir build
}

package() {
	DESTDIR="${pkgdir}" cmake --install build
}
