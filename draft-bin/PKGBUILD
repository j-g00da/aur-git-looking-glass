# Maintainer: larte <balkian@gmail.com>

pkgname=draft-bin
pkgdesc="Draft client"
pkgver=0.17.6
pkgrel=1
arch=('x86_64' 'aarch64')
url="http://draft.sh"
license=('mit')
conflicts=()
_draft_file=draft-$pkgver
source_x86_64=($_draft_file::https://github.com/Azure/draft/releases/download/v0.17.6/draft-linux-amd64 )
source_aarch64=($_draft_file::https://github.com/Azure/draft/releases/download/v0.17.6/draft-linux-arm64 )
md5sums_x86_64=('de77390d33a13a32c4de2b7b10df2ca8')
md5sums_aarch64=('180f700055ad0fc4a6e72c6ee246f07d')

package() {
  install -Dm 755 "$srcdir/draft-$pkgver" "$pkgdir/usr/bin/draft"
}
