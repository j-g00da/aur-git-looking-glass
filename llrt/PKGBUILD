# Maintainer: Jason Go <jasongo@jasongo.net>

_sdk='std-sdk'
_suffix="$( [ "$_sdk" == "std-sdk" ] && echo "" || echo "-$_sdk" )"
pkgname="llrt$_suffix"
pkgver=0.7.0beta
pkgrel=20
pkgdesc='Lightweight JavaScript runtime, compiler, REPL, and test runner (STANDARD @aws-sdk bundled)'
arch=('x86_64' 'aarch64')
url='https://github.com/awslabs/llrt'
license=('Apache-2.0')
makedepends=('cmake' 'nodejs' 'rustup' 'zig' 'zip' 'zstd')
optdepends=(
  'typescript: transpiler for TypeScript code with type checking support'
  'esbuild: fast compiler and bundler for JavaScript and TypeScript'
  'swc-js-bin: drop-in replacement for Babel with compilation and polyfill support'
  'bun-bin: fast runtime, compiler, and bundler for JavaScript and TypeScript'
)
provides=('llrt')
conflicts=('llrt')
options=(!buildflags !makeflags !debug)
source=(
  "git+$url.git#tag=v${pkgver//beta/-beta}"
  "https://github.com/yarnpkg/yarn/releases/download/v1.22.22/yarn-v1.22.22.tar.gz"
)
sha256sums=(
  '20058c4d89e6f1675885b835aef2d3215b85fa0d55bba62d07de5481aa847e5d'
  '88268464199d1611fcf73ce9c0a6c4d44c7d5363682720d8506f6508addf36a0'
)

_CARCH="$( [ "$CARCH" == "aarch64" ] && echo "arm64" || echo "x64" )"

prepare() {
  # Use locally installed Yarn to prevent conflict with extra/corepack, extra/yarn, or any other globally installed Yarn
  bsdtar zvxf yarn-v1.22.22.tar.gz

  cd llrt

  # Use Rust's nightly version from the date of the upstream release to prevent regression issues
  sed -i "s/RUST_VERSION = nightly/RUST_VERSION = nightly-2025-09-23/g" Makefile

  rustup install nightly-2025-09-23 &
  task1=$!

  git submodule update --init --checkout &
  task2=$!

  "$srcdir/yarn-v1.22.22/bin/yarn" &
  task3=$!

  wait $task1
  wait $task2
  wait $task3
}

build() {
  cd llrt
  make "stdlib-$_CARCH" && make "libs-$_CARCH"
  make "llrt-linux-$_CARCH$_suffix.zip"
}

package() {
  install -Dm755 "$srcdir/llrt/target/$CARCH-unknown-linux-musl/release/llrt" "$pkgdir/usr/bin/llrt"
  ln -sf "/usr/bin/llrt" "$pkgdir/usr/bin/llrt-$_sdk" # Provide a suffixed alias to llrt
  install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" "$srcdir/llrt/"{LICENSE,THIRD_PARTY_LICENSES,NOTICE}
}
