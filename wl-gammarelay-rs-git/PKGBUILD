_pkgname=wl-gammarelay-rs
pkgname=${_pkgname}-git
pkgver=v1.0.0.r0.ge389544
pkgrel=1
pkgdesc="A simple program that provides DBus interface to control display temperature and brightness under wayland without flickering"
makedepends=('cargo')
conflicts=(${_pkgname})
arch=('x86_64')
url="https://github.com/MaxVerevkin/wl-gammarelay-rs"
license=('GPL-3.0-only')
source=(
  "git+$url.git"
)
sha256sums=(
  'SKIP'
)

pkgver() {
  cd ${srcdir}/${_pkgname}
  git describe --long --tags --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd ${srcdir}/${_pkgname}
  export RUSTUP_TOOLCHAIN=stable
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd ${srcdir}/${_pkgname}
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  export RUSTFLAGS=-Awarnings       # Suppress warnings, as build generates a lot of then and they are not relevant to end user
  cargo build --frozen --release --all-features
}

package() {
  cd ${srcdir}/${_pkgname}
  install -Dm0755 -t "$pkgdir/usr/bin/" target/release/${_pkgname}
}
