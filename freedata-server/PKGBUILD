# Maintainer: Petr Kracik <petrkr@petrkr.net>

pkgname=freedata-server
pkgver=0.17.8
pkgrel=1
pkgdesc="FreeDATA is an open-source HF communication platform using Codec2 data modes for global digital messaging. It offers a server-client architecture, REST API and a messaging system."
arch=('x86_64')
url="https://wiki.freedata.app"
license=('GPL-3.0')
depends=('uvicorn'
	'python-pyserial'
	'python-numpy'
	'python-psutil'
	'python-sqlalchemy'
	'python-requests'
	'python-websocket-client'
	'python-fastapi'
	'python-structlog'
	'python-sounddevice')
optdepends=('freedata-gui: Add Web based GUI interface for server'
	'hamlib: Can use local RIG control')
install=freedata.install
makedepends=('cmake'
	'make'
	'gcc')

_codec2_commit="ff00a6e2489f870abb10117ff5bf4b0a64bf05d4"
source=("freedata.install"
	"FreeDATA.desktop"
	"freedata.sh"
	"https://github.com/DJ2LS/FreeDATA/archive/refs/tags/v${pkgver}.tar.gz"
	"https://github.com/drowe67/codec2/archive/${_codec2_commit}.zip")

sha256sums=('7d9b5e2cca9c7f2ee2c6beada910c0e0e0362879a10cba671e9a80247456af1d'
            '3fe415e43c909c21af1128cf2b5892d9ee3c2f39557644b228432f5d6e62da8a'
            'f6c2ab5e77ae21306337094eda4f4d4c251845a4152b50a3938750fccacd61c4'
            'de5c6159dddfe8ca3c4de82b16bc95ebe336d925c38714a49e993dc9ff781ee9'
            '40ede4f9240d6082c49483ccfa6a7f616c09d52a3715bd837f30563301c45e42')


build() {
	cd "${srcdir}"
	
	# Build codec2
	cd codec2-${_codec2_commit}
	[ -d build ] && rm -r build
	mkdir build
	cd build
	cmake ..
	make codec2 -j4
	cd ../../
	cd FreeDATA-${pkgver}/freedata_server
	python3 -m compileall .
	rm -r lib/codec2
	cd ../freedata_gui

}

package() {
	cd ${pkgdir}
	mkdir -p "usr/bin"
	mkdir -p "opt/FreeDATA"
	mkdir -p "usr/share/doc"
	mkdir -p "usr/share/licenses/${pkgname}"
	mkdir -p "usr/share/applications"
	mkdir -p "usr/share/icons/hicolor/192x192/apps"

	cd ${pkgdir}/opt/FreeDATA
	
	# Copy server
	cp -a ${srcdir}/FreeDATA-${pkgver}/freedata_server ./
	
	# Copy own codec2
	cp ${srcdir}/codec2-${_codec2_commit}/build/src/libcodec2.so* ./freedata_server/lib/

	# Copy desktop icon
	cp ${srcdir}/FreeDATA-${pkgver}/freedata_gui/public/android-chrome-192x192.png ${pkgdir}/usr/share/icons/hicolor/192x192/apps/FreeDATA.png

	# Copy desktop link
	cp ${srcdir}/FreeDATA.desktop ${pkgdir}/usr/share/applications/

	# Copy License and documentation
	cp ${srcdir}/FreeDATA-${pkgver}/LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/
	cp -a ${srcdir}/FreeDATA-${pkgver}/documentation ${pkgdir}/usr/share/doc/${pkgname}

	install -m 755 ${srcdir}/freedata.sh ${pkgdir}/usr/bin/freedata
}
