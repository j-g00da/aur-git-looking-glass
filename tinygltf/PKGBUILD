# Maintainer: Ali Emre Gülcü <aliemreglc at gmail dot com>
# Update PKGSums: updpkgsums
# Update SRCINFO: makepkg --printsrcinfo > .SRCINFO

pkgname=tinygltf
pkgver=2.9.6
pkgrel=1
pkgdesc="Header only C++ tiny glTF library(loader/saver)"
arch=('any')
url="https://github.com/syoyo/$pkgname"
license=('MIT')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('ba2c47a095136bfc8a5d085421e60eb8e8df3bca4ae36eb395084c1b264c6927')

package() {
  cd $pkgname-$pkgver
  mkdir -p $pkgdir/usr/include/$pkgname $pkgdir/usr/share/licenses/$pkgname
  install *.h $pkgdir/usr/include/$pkgname
  install *.hpp $pkgdir/usr/include/$pkgname
  install LICENSE $pkgdir/usr/share/licenses/$pkgname
}
