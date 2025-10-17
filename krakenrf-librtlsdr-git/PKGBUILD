# Maintainer: Vladyslav Aviedov <aur at vladaviedov dot org>
pkgname=krakenrf-librtlsdr-git
_gitname=librtlsdr
pkgver=r657.ea7baad
pkgrel=1
pkgdesc='Software to turn the RTL2832U into an SDR (for KrakenSDR)'
arch=('x86_64')
url='https://github.com/krakenrf/librtlsdr'
provides=('krakenrf-librtlsdr')
conflicts=('rtl-sdr' 'krakenrf-librtlsdr')
depends=('glibc' 'libusb')
makedepends=('git' 'cmake')
license=('GPL-2.0-only')
source=("git+${url}.git")
sha1sums=('SKIP')

pkgver() {
	cd "${srcdir}/${_gitname}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "${srcdir}/${_gitname}"

	mkdir -p build
	cd build
	cmake .. \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DCMAKE_BUILD_TYPE=Release \
		-DDETACH_KERNEL_DRIVER=ON \
		-DCMAKE_POLICY_VERSION_MINIMUM=3.5 \
		-Wno-dev

	cmake --build .
}

package() {
	cd "${srcdir}/${_gitname}/build"
	make DESTDIR="${pkgdir}" install
	install -D -m644 "${srcdir}/${_gitname}/rtl-sdr.rules" "${pkgdir}/usr/lib/udev/rules.d/10-rtl-sdr.rules"
	install -D -m644 "${srcdir}/${_gitname}/rtlsdr-blacklist.conf" "$pkgdir/etc/modprobe.d/rtlsdr.conf"
}
