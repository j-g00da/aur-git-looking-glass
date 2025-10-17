# Maintainer: Lili1228 <aur at lili dot lgbt>
pkgname=86box-roms
pkgver=5.1
pkgrel=1
pkgdesc='ROMs for the 86Box emulator'
arch=('any')
url='https://github.com/86Box/roms'
license=('custom')
options=('!strip')
source=("https://github.com/86Box/roms/archive/refs/tags/v${pkgver}.tar.gz")
sha512sums=('f03d15265d2da2e2fa2bded9fbf1f401e595d766e1b3932bbba17817cd55afdf4e6e4c4caa97433ee4ca17ae33df386ccf6814374345bb6e8e4c47cf8178c653')

package() {
    cd "${srcdir}/roms-${pkgver}"
    install -d "$pkgdir/usr/share/86Box/roms"
    cp -R [a-z]* "$pkgdir/usr/share/86Box/roms"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
