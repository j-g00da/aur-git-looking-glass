# Maintainer: Nihal Kumar <2tv8xupqg at mozmail dot com>
pkgname=contextpilot
pkgver=0.9.2
pkgrel=1
pkgdesc="Analyze Git blame information, infer code context, and index your codebase for deep, fine-grained search and navigation."
arch=('x86_64' 'aarch64')
url="https://github.com/krshrimali/context-pilot-rs"
license=('MIT')
depends=('git')
makedepends=('rust')
optdepends=('neovim: For neovim integration'
  'visual-studio-code-bin: For VSCode integration')
provides=("$pkgname")
conflicts=("$pkgname")
replaces=("context-pilot")
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('2e6fc7aea5df34075291e3ec93b7936f782237c8580a5cae7a8b716b8da4c9c3')

prepare() {
  cd "$srcdir/context-pilot-rs-$pkgver"
  case "$CARCH" in
  armv7h) target="armv7-unknown-linux-gnueabihf" ;;
  aarch64) target="aarch64-unknown-linux-gnu" ;;
  *) target="$CARCH-unknown-linux-gnu" ;;
  esac
  cargo fetch --target "$target"
}

build() {
  cd "$srcdir/context-pilot-rs-$pkgver"
  cargo build --release
}

package() {
  cd "$srcdir/context-pilot-rs-$pkgver"
  install -Dm755 "target/release/contextpilot" "$pkgdir/usr/bin/$pkgname"
}
