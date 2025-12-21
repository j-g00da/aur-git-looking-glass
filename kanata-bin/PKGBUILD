# Maintainer: Breno Ramalho Lemes <breno@br-lemes.net>
pkgname=kanata-bin
pkgver=1.10.1
pkgrel=1
pkgdesc='Improve keyboard comfort and usability with advanced customization'
arch=('x86_64')
url='https://github.com/jtroo/kanata/'
license=('LGPL-3.0-only')
provides=('kanata')
depends=('gcc-libs' 'glibc')
source=(
	"https://github.com/jtroo/kanata/releases/download/v${pkgver//_/-}/kanata-linux-binaries-v${pkgver//_/-}-x64.zip"
	'https://github.com/jtroo/kanata/raw/main/LICENSE'
)
sha256sums=(
	'f755a4bdeb26821893ef954732db34eda845dcecd421c6f06a8b4b280ea38a39'
	'a5681bf9b05db14d86776930017c647ad9e6e56ff6bbcfdf21e5848288dfaf1b'
)

package() {
	install -Dm755 "${srcdir}/kanata_linux_x64" "${pkgdir}/usr/bin/kanata"
	install -Dm755 "${srcdir}/kanata_linux_cmd_allowed_x64" "${pkgdir}/usr/bin/kanata_cmd_allowed"
	install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
