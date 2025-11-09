# Maintainer : bartus <arch-user-repoᘓbartus.33mail.com>
# Contributor : N30N <archlinux@alunamation.com>
# Contributor : Wenzel Jakob <wenzel@mitsuba-renderer.org>

_pkgname="collada-dom"
pkgname="${_pkgname}-mitsuba"
pkgver=2.4.0
pkgrel=3
pkgdesc="An API that provides a C++ object representation of a COLLADA XML instance document (required for mitsuba renderer)."
url="http://collada-dom.sourceforge.net/"
license=("MIT")
arch=("i686" "x86_64")
depends=("libxml2" "boost-libs" "pcre" "minizip")
makedepends=("boost")
source=("http://downloads.sourceforge.net/${_pkgname}/collada-dom-${pkgver}.tgz"
        "0001-fix-return-type-thanks-to-22.patch"
        "fix-minizip-include-path.patch"
        "$pkgname-fix-boost1.85.patch::https://github.com/rdiankov/collada-dom/pull/43.patch"
        "boost-1.89.patch"
       )
md5sums=('20399de4206eab850c32e65c04e907cb'
         'ebfba4cccb6a0862de2df286603a0c80'
         'a907fc4cdade0b368f7bd2e25f1846c4'
         'e424390147c45e62ca81e77366ec9cfb'
         'a7739d0efd3c2bd0e56bdb542053a46a')

prepare() {
	cd ${_pkgname}-${pkgver}
	printf "${srcdir}/%s\n" "${source[@]}"|\
	grep -Po '^.*?(patch|diff)(?=::|$)'|\
	xargs -l patch -Np1 -i
}

build() {
	cd ${_pkgname}-${pkgver}/dom
	sed -i.bak "s/domMinorVersion := 2/domMinorVersion := 4/g" Makefile
	rm -Rf external-libs
	make project=dom libOpts="-lpcre -lpcrecpp -Lbuild/linux-1.4 -lxml2 -I/usr/include/minizip -lminizip -Wl,-soname -Wl,libcollada14dom.so.2.4"  ccFlags="-DDOM_INCLUDE_LIBXML -DCOLLADA_DOM_SUPPORT141 -fPIC -DDOM_INCLUDE_LIBXML -O3"
}

package() {
	cd ${_pkgname}-${pkgver}/dom

	install -d ${pkgdir}/usr/lib ${pkgdir}/usr/include
	make prefix=${pkgdir}/usr project=dom install
	mv ${pkgdir}/usr/include/colladadom ${pkgdir}/usr/include/collada-dom-mitsuba

	install -D -m644 license.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim: set noet ff=unix:
