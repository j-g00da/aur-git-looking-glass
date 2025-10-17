# Submitter: AtticFinder65536 <atticfinder -AT- rocklabs -DOT- xyz>
# Maintainer: aik2 <aik2mlj -AT- gmail -DOT- com>

pkgname=('otf-nasin-nanpa')
pkgver=4.0.2
pkgrel=1
pkgdesc="A font for the sitelen pona writing system with UCSUR and ligature support"
url="https://github.com/ETBCOR/nasin-nanpa"
license=('MIT')
source=("$url/releases/download/n${pkgver}/nasin-nanpa-${pkgver}.otf"
    # "$url/releases/download/n${pkgver}/nasin-nanpa-${pkgver}-UCSUR.otf"
    # "$url/releases/download/n${pkgver}/nasin-nanpa-${pkgver}-Helvetica.otf"
    "$url/raw/n${pkgver}/LICENSE")
sha256sums=('7963dc154a34c84dabe1c2f793214171d1e9d1104a505de4818a95e41e79c343'
    # 'f43918ef06c1db6205b0800083283c81800ba647d138acf3739021a582adea82'
    # '8acb5e503a60747b9f5d891c6ec0bbc1b4fe7b82f302b15ee364f0f707e3d381'
    '2bb13a795d1d7f6df0288e228f29e4250e6a0e9b11f90044a737cc024002d6ab')

arch=('any')

package() {
    # Install license
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

    # Install font
    install -Dm644 -T nasin-nanpa-${pkgver}.otf "${pkgdir}/usr/share/fonts/OTF/nasin-nanpa.otf"
    # install -Dm644 -T nasin-nanpa-${pkgver}-UCSUR.otf "${pkgdir}/usr/share/fonts/OTF/nasin-nanpa-UCSUR.otf"
    # install -Dm644 -T nasin-nanpa-${pkgver}-Helvetica.otf "${pkgdir}/usr/share/fonts/OTF/nasin-nanpa-Helvetica.otf"
}
