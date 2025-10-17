# Maintainer: Nihal Kumar <2tv8xupqg at mozmail dot com>
pkgname=contextpilot-git
pkgver=0.9.1.r0.g917812a
pkgrel=1
pkgdesc="Analyze Git blame information, infer code context, and index your codebase for deep, fine-grained search and navigation."
arch=('x86_64' 'aarch64')
url="https://github.com/krshrimali/context-pilot-rs"
license=('MIT')
depends=('git')
makedepends=('rust')
optdepends=('neovim: For neovim integration'
  'visual-studio-code-bin: For VSCode integration')
provides=("contextpilot")
conflicts=("contextpilot")
replaces=("context-pilot")
source=("git+$url.git")
sha256sums=('SKIP')

pkgver() {
  cd "context-pilot-rs"
  git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "$srcdir/context-pilot-rs"
  case "$CARCH" in
    armv7h) target="armv7-unknown-linux-gnueabihf" ;;
    aarch64) target="aarch64-unknown-linux-gnu" ;;
    *) target="$CARCH-unknown-linux-gnu" ;;
  esac
  cargo fetch --target "$target"
}

build() {
  cd "$srcdir/context-pilot-rs"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR="target"
  cargo build --release
}

package() {
  cd "$srcdir/context-pilot-rs"
  install -Dm755 "target/release/contextpilot" "$pkgdir/usr/bin/contextpilot"
}
