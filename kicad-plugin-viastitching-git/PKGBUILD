# Maintainer: Vladyslav Aviedov <aur at vladaviedov dot org>
pkgname=kicad-plugin-viastitching-git
_pkgname=viastitching
pkgver=r132.0e23cd9
pkgrel=1
pkgdesc='ViaStitching action-plugin for KiCAD'
arch=('any')
url='https://github.com/weirdgyn/viastitching'
license=('MIT')
makedepends=('git')
depends=('kicad' 'python' 'python-wxpython' 'python-numpy')
provides=('kicad-plugin-viastitching')
conflicts=('kicad-plugin-viastitching')
source=("git+${url}")
sha256sums=('SKIP')

pkgver() {
	cd "${srcdir}/${_pkgname}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
	cd "${srcdir}/${_pkgname}"

	mkdir -p "${pkgdir}/usr/share/kicad/scripting/plugins/viastitching"
	install -Dm644 *.py "${pkgdir}/usr/share/kicad/scripting/plugins/viastitching"
	install -Dm644 defaults.json viastitching.png viastitching.fbp "${pkgdir}/usr/share/kicad/scripting/plugins/viastitching"

	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
