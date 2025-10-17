# Maintainer: Vladyslav Aviedov <aur at vladaviedov dot org>
# Contributor: Yamada Hayao <hayao at fascode.net>
pkgname="rofi-themes-collection-git"
_pkgname=${pkgname%-git}
pkgver=r27.ec731ce
epoch=1
pkgrel=2
pkgdesc='Themes Collection for Rofi Launcher'
arch=('any')
url='https://github.com/newmanls/rofi-themes-collection'
license=('GPL-3.0-only')
depends=('rofi')
makedepends=('git')
source=("git+$url")
sha256sums=('SKIP')

pkgver() {
	cd "${srcdir}/${_pkgname}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package(){
	cd "${srcdir}/${_pkgname}"
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
	install -Dm644 README.md "${pkgdir}/usr/share/doc/${_pkgname}/README.md"
	find themes -type f -exec install -Dm644 {} "${pkgdir}/usr/share/rofi/{}" \;
}
