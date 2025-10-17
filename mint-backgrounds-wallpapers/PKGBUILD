# Maintainer: Markus Pesch <markus.pesch@cryptic.systems>

pkgname=mint-backgrounds-wallpapers
pkgver=1.0
pkgrel=1
pkgdesc="The backgrounds included in Linux Mint 22.1 wallpapers"
license=('Various')
arch=('any')
url="http://packages.linuxmint.com/pool/main/m/${pkgname}"
source=("${url}/${pkgname}_$pkgver.tar.gz")
sha256sums=('6059e3a28671a7d7ef385191efb056750362e3e2c45a731f130075d1adf4e302')
replaces=(
  "mint-backgrounds-xia"
)
conflicts=(
  "mint-backgrounds-xia"
)

package() {
  mkdir --parents ${pkgdir}/usr/share/backgrounds/linuxmint-wallpapers
  mkdir --parents ${pkgdir}/usr/share/{cinnamon-background-properties,gnome-background-properties,mate-background-properties}

  cp --archive ${srcdir}/${pkgname}/backgrounds/linuxmint-wallpapers ${pkgdir}/usr/share/backgrounds
  cp --archive ${srcdir}/${pkgname}/cinnamon-background-properties/* ${pkgdir}/usr/share/cinnamon-background-properties
  cp --archive ${srcdir}/${pkgname}/gnome-background-properties/* ${pkgdir}/usr/share/gnome-background-properties
  cp --archive ${srcdir}/${pkgname}/mate-background-properties/* ${pkgdir}/usr/share/mate-background-properties
}
