# Maintainer: asm0dey <me@asm0dey.site>
pkgname=unregistry
pkgver=0.3.0
pkgrel=1
pkgdesc="Push docker images directly to remote servers without an external registry"
arch=(any)
url="https://github.com/psviderski/unregistry/"
license=('Apache-2.0')
source=("docker-pussh-$pkgver::https://raw.githubusercontent.com/psviderski/unregistry/refs/tags/v$pkgver/docker-pussh")
sha256sums=('38f8f9c989a3ff571bc2540d03ec3d006da3b8706a3d4c57ed3c95d58944c57d')
depends=(docker bash)

package() {
    install -dm 755 $pkgdir/usr/lib/docker/cli-plugins
    install -m 755 "$srcdir/docker-pussh-$pkgver" $pkgdir/usr/lib/docker/cli-plugins/docker-pussh
}
