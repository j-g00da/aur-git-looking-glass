# Maintainer: Ali Emre Gülcü <aliemreglc at gmail dot com>

pkgname=cgltf
pkgver=1.15
pkgrel=1
pkgdesc="Single-file/stb-style C glTF loader and writer"
arch=('any')
url="https://github.com/jkuhlmann/$pkgname"
license=('MIT')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
md5sums=('afc72f494447d0d288b1887ea5dcc53b')

package() {
  cd $pkgname-$pkgver
  mkdir -p $pkgdir/usr/include/$pkgname $pkgdir/usr/share/licenses/$pkgname
  install *.h $pkgdir/usr/include/$pkgname
  install LICENSE $pkgdir/usr/share/licenses/$pkgname
}
