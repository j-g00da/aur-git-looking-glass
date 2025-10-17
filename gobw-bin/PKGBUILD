# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=gobw
pkgname=$_projectname-bin
pkgver=1.0
pkgrel=2
pkgdesc="Bitwarden TUI written in Go"
arch=("x86_64")
url="https://github.com/007Psycho007/gobw"
license=("GPL-3.0-only")
depends=("bitwarden-cli")
provides=("gobw")
conflicts=("gobw")
source=("$_projectname-$pkgver.tar.gz::$url/releases/download/$pkgver/${_projectname}_${pkgver}_linux_amd64.tar.gz")
b2sums=('13386629a51605aab7bcc1e9a54736d170876803e0ac4800e4bbc997b55df6edcb33ce16cef6b7b11be2a8dd07af2a459ce991c378648de533d3b0d7bccd37a1')

package() {
    install -Dm 0755 gobw "${pkgdir}/usr/bin/gobw"
    install -Dm 0644 LICENSE "${pkgdir}/usr/share/licenses/${_projectname}/LICENSE"
    install -Dm 0644 README.md "${pkgdir}/usr/share/doc/${_projectname}/README.md"
}
