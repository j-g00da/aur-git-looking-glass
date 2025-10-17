# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=git-sv
pkgver=2.0.1 # renovate: datasource=github-releases depName=thegeeklab/git-sv extractVersion='^v?(?<version>.*)$'
pkgrel=1
pkgdesc="Semantic versioning tool for git based on conventional commits "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/thegeeklab/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('e9fff2eeb7d7dae04dc9053f72a5a5a6d685922ef91496e43032ccf4ef910b71f93ddf01f4a08a661ad105c582eeac51cd47da85a1d70401ad524179f1bf1826')
b2sums=('76d2a0999f57df7b19109674ae5789aca1fec4b6b4a28c414cc2a438639def47f4174d53d78dd426b712d2521a1425757ce95270edb3b2dcdea3d08522105a7b')

build() {
  make --directory "$pkgname-$pkgver" build
}

package() {
  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$pkgname-$pkgver/cmd/$pkgname/$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE"
}
