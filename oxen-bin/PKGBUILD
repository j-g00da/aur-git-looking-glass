# Maintainer: Nero Blackstone <gf7600gs@gmail.com>

pkgname=oxen-bin
pkgver=0.36.4
pkgrel=2
pkgdesc="Oxen CLI. Oxen is a lightning fast data version control system for structured and unstructured machine learning datasets."
arch=('x86_64')
url="https://www.oxen.ai/"
license=('Apache-2.0')
source=("https://github.com/Oxen-AI/Oxen/releases/download/v${pkgver}/oxen-linux-x86_64.deb")
sha256sums=('21bd92fed0fda5f407e3ab945e96c8316fb9bcf3358eda6a27de521afa5951f8')

package() {
    cd "$srcdir"
    ar x oxen-linux-x86_64.deb
    tar -xf data.tar.* -C "$pkgdir"
}