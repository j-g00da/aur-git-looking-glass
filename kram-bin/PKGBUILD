# Maintainer: mirsella <mirsella@protonmail.com>
pkgname=kram-bin
pkgver=1.7.30
pkgrel=1
pkgdesc="Encode/decode/info to KTX/KTX2/DDS files with LDR/HDR and BC/ASTC/ETC2"
arch=('x86_64')
url="https://github.com/alecazam/kram"
license=('MIT')
depends=('unzip')
source=("${pkgname}-${pkgver}.zip::https://github.com/alecazam/kram/releases/download/v${pkgver}/kram-linux.zip")
sha256sums=('039101fcdeef246564dcedbd881832222073ae50db03ade71140ad1a0e07e576')

package() {
	cd "${srcdir}"

	unzip "${pkgname}-${pkgver}.zip" -d "${pkgname}-${pkgver}"

	install -Dm755 "${pkgname}-${pkgver}/kram" "${pkgdir}/usr/bin/kram"

	if [[ -f "${pkgname}-${pkgver}/LICENSE" ]]; then
		install -Dm644 "${pkgname}-${pkgver}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	fi
}
