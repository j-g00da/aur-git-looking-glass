# Maintainer: Nino K. <aur@assyt.fi>

pkgname=flumi-bin
_pkgname=Flumi.x86_64

pkgver=1.0.2
pkgrel=1
epoch=1
pkgdesc='The wayfinder (browser) for Gurted, a "web ecosystem".'
arch=('x86_64')
url="https://github.com/outpoot/gurted"
license=('CC BY-NC 4.0')
depends=('glibc')

provides=()
conflicts=()
replaces=()

source=("https://github.com/outpoot/gurted/releases/download/v$pkgver/Flumi_Linux.tar.gz" "$pkgname.desktop")
sha256sums=("c51c92912e292820583fb875e55b81c28bd8197db2affb978e0d245278b72d88" "19befd866c5deafebd476545f12df46e0db8ff2223709bad7b30978596a4336b")

package() {
	mkdir -p "$pkgdir"/usr/bin
	mkdir -p "$pkgdir"/usr/share/applications
	mkdir -p "$pkgdir"/opt

	cp -r . "$pkgdir"/opt/$pkgname

	#very bad hardcoding the archive name dont like this
	rm "$pkgdir"/opt/$pkgname/Flumi_Linux.tar.gz

	chmod +x "$pkgdir"/opt/$pkgname/$_pkgname

	ln -s /opt/$pkgname/$_pkgname "$pkgdir"/usr/bin/$pkgname

	
	cp $pkgname.desktop "$pkgdir"/usr/share/applications/$pkgname.desktop
}
