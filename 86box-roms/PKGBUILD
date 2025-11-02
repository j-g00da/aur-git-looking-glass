# Maintainer: Lili1228 <aur at lili dot lgbt>
pkgname=86box-roms
pkgver=5.2
pkgrel=1
pkgdesc='ROMs for the 86Box emulator'
arch=('any')
url='https://github.com/86Box/roms'
license=('custom')
options=('!strip')
source=("https://github.com/86Box/roms/archive/refs/tags/v${pkgver}.tar.gz")
sha512sums=('3776858f2a90d001fec0c7898df3f0f7459e4a39adc553e35f92d369a10446fb79a1e41e6c11a915f23169098f5ae1be8d3c5c98f2cfac0a1db04d664aa60440')

package() {
    cd "${srcdir}/roms-${pkgver}"
    install -d "$pkgdir/usr/share/86Box/roms"
    cp -R [a-z]* "$pkgdir/usr/share/86Box/roms"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
