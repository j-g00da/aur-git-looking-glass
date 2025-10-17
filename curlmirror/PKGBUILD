# Contributor: sekret <sekret at posteo dot se>
# Contributor: Lex Black <autumn-wind at web dot de>
# Contributor: rabyte <rabyte__gmail>

pkgname=curlmirror
pkgver=20150310
pkgrel=4
pkgdesc="Mirrors a web site by using curl to download each page"
arch=('any')
url="https://github.com/cudeso/tools/blob/master/curlmirror.txt"
# linked from https://curl.se/docs/programs.html
license=('Unlicense')
depends=('curl' 'perl')
makedepends=('dos2unix')
source=(${pkgname}-${pkgver}.txt::https://github.com/cudeso/tools/raw/master/${pkgname}.txt)
md5sums=('14c8928d727e08d023a6325e0ec5af3f')


prepare() {
  dos2unix -n ${pkgname}-${pkgver}.txt ${pkgname}
}

package() {
  install -Dm755 "${pkgname}" -t "$pkgdir/usr/bin/"
}

# vim:set ts=2 sw=2 et:
