# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=reddit-tui
pkgname=$_projectname-bin
pkgver=0.3.9
pkgrel=2
pkgdesc="Terminal UI for Reddit"
arch=("x86_64")
url="https://github.com/tonymajestro/reddit-tui"
license=("MIT")
provides=("reddit-tui")
conflicts=("reddit-tui")
source=("$_projectname-$pkgver.tar.gz::$url/releases/download/v$pkgver/${_projectname}_Linux_x86_64.tar.gz")
b2sums=('c9a7c682b743f332a6430c621ab2eea21065482a0a8a755d97f89cad4762deb112fa567603e0136521665327b011b8912713122d80bec31a721264745126b438')

package() {
    install -Dm 0755 reddittui "${pkgdir}/usr/bin/reddittui"
    install -Dm 0644 LICENSE.txt "${pkgdir}/usr/share/licenses/${_projectname}/LICENSE.txt"
    install -Dm 0644 README.md "${pkgdir}/usr/share/doc/${_projectname}/README.md"
}
