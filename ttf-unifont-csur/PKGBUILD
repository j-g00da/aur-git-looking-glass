# Maintainer: Gregory G Danielson III <gregdan3@protonmail.com>

pkgname=ttf-unifont-csur
pkgver=17.0.03
pkgrel=1
pkgdesc="TrueType part of the GNU Unifont containing Michael Everson's ConScript Unicode Registry (CSUR) Private Use Area (PUA) glyphs"
url="http://unifoundry.com/unifont.html"
arch=('any')
license=('GPL')
depends=('ttf-unifont')
makedepends=('fontforge')
url=https://unifoundry.com/unifont/index.html
source=(
	"http://unifoundry.com/pub/unifont/unifont-${pkgver}/unifont-${pkgver}.tar.gz"{,.sig}
)
sha512sums=('70ebb98fe81b8e89d887002be5bdcd7e396cdc21f6404013f9a4b667c61c7c5967c905039d55c45f2455e653c6dfe3284dd62841697a17d4d2d6ef9c9b5ad464'
            'SKIP')
validpgpkeys=('95D2E9AB8740D8046387FD151A09227B1F435A33') # Paul Hardy <com dot unifoundry at unifoundry>

build() {
	cd "${srcdir}/unifont-${pkgver}/font"
	make hex
	make csurttf
}

package() {
	cd "$srcdir"
	install -Dm644 "unifont-${pkgver}/font/compiled/unifont_csur-${pkgver}.ttf" "${pkgdir}/usr/share/fonts/TTF/Unifont_CSUR.ttf"
}
