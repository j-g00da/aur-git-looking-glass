# Maintainer: Breno Ramalho Lemes <breno@br-lemes.net>
pkgname=kanata-bin
pkgver=1.9.0
pkgrel=1
pkgdesc='Improve keyboard comfort and usability with advanced customization'
arch=('x86_64')
url='https://github.com/jtroo/kanata/'
license=('LGPL-3.0-only')
provides=('kanata')
depends=('gcc-libs' 'glibc')
source=(
	"kanata-${pkgver}::https://github.com/jtroo/kanata/releases/download/v${pkgver//_/-}/kanata"
	"kanata_cmd_allowed-${pkgver}::https://github.com/jtroo/kanata/releases/download/v${pkgver//_/-}/kanata_cmd_allowed"
	'https://github.com/jtroo/kanata/raw/main/LICENSE'
)
sha256sums=(
	'440ce0f754adc32b1e9d0f47c0016c59222eaad7c1b2c86ce19f2559e4d54ffa'
	'947563c29394955f033c0d749446f7b7cd60279b7b96cd7eb51011e2cbea1aaf'
	'a5681bf9b05db14d86776930017c647ad9e6e56ff6bbcfdf21e5848288dfaf1b'
)

package() {
	install -Dm755 "kanata-${pkgver}" "${pkgdir}/usr/bin/kanata"
	install -Dm755 "kanata_cmd_allowed-${pkgver}" "${pkgdir}/usr/bin/kanata_cmd_allowed"
	install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
