# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=git-sv
pkgver=2.0.6 # renovate: datasource=github-releases depName=thegeeklab/git-sv extractVersion='^v?(?<version>.*)$'
pkgrel=1
pkgdesc="Semantic versioning tool for git based on conventional commits "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/thegeeklab/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('babad59965a5409ea5f8ca3cfce5019ef140e54140516794bb1e86fa5c7a7b92549f78820053d96d465166c7e4d7674c0016ca233fecc23b5f3637f9666cfa19')
b2sums=('b0d9764ad3ee5019b9dfa1db938b514ad93043c0fe5ad3f69b18f3c5af45fab75684399f85b44d2a8b9bcdf4de0885b13b56102c25fb903e60692f239e768ad4')

build() {
  make --directory "$pkgname-$pkgver" build
}

package() {
  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$pkgname-$pkgver/dist/$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE"
}
