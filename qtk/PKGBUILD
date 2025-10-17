# Maintainer: qsqcqs
pkgname='qtk'
pkgver=mau
pkgrel=1
pkgdesc="random qol stuff"
arch=('x86_64')
url="https://github.com/qsqcqs/qtk"
license=('GPL-3.0-or-later')
depends=('python3')
checkdepends=()
optdepends=()
source=("https://github.com/qsqcqs/$pkgname/archive/refs/tags/$pkgver-$pkgrel.tar.gz")
noextract=()
validpgpkeys=()


package() {
	cd "$pkgname-$pkgver-$pkgrel"
	mkdir "${pkgdir}"/usr/bin/qtk
    install -Dm644 zwnj "${pkgdir}"/usr/bin/zwnj
    install -Dm644 epscol "${pkgdir}"/usr/bin/epscol
	install -Dm644 nya~ "${pkgdir}"/usr/bin/nya~
	    install -Dm644 nyom~ "${pkgdir}"/usr/bin/nyom~
	    install -Dm644 flynx "${pkgdir}"/usr/bin/flynx
	    install -Dm644 stop "${pkgdir}"/usr/bin/stop
    install -Dm644 cont "${pkgdir}"/usr/bin/cont
    install -Dm644 bin "${pkgdir}"/usr/bin/qtk/bin
    chmod +x "${pkgdir}"/usr/bin/zwnj
    chmod +x "${pkgdir}"/usr/bin/epscol
	chmod +x "${pkgdir}"/usr/bin/nya~
    chmod +x "${pkgdir}"/usr/bin/nyom~
   chmod +x "${pkgdir}"/usr/bin/stop
   chmod +x "${pkgdir}"/usr/bin/cont
   chmod +x "${pkgdir}"/usr/bin/flynx

#add /bin/wifi sometime
}



sha256sums=('9aaed7c3d983cbf00c6617a7267002966574ea576f69d553eed2a1e952b897b6')
