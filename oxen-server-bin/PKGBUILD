# Maintainer: Nero Blackstone <gf7600gs@gmail.com>

pkgname=oxen-server-bin
pkgver=0.36.4
pkgrel=2
pkgdesc="Oxen server. Oxen is a lightning fast data version control system for structured and unstructured machine learning datasets."
arch=('x86_64')
url="https://www.oxen.ai/"
license=('Apache-2.0')
source=("https://github.com/Oxen-AI/Oxen/releases/download/v${pkgver}/oxen-server-linux-x86_64.deb")
sha256sums=('49986b6d4a16c1041471ac05438275506ea753720ed07092855a7cd192877961')

package() {
    cd "$srcdir"
    ar x oxen-server-linux-x86_64.deb
    tar -xf data.tar.* -C "$pkgdir"
}