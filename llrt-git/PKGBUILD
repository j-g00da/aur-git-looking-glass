# Maintainer: Jason Go <jasongo@jasongo.net>

_rust_version='nightly'
_sdk='std-sdk'
_suffix="$( [ "$_sdk" == "std-sdk" ] && echo "" || echo "-$_sdk" )"
pkgname="llrt$_suffix-git"
pkgver=20251121.200859
pkgrel=1
pkgdesc='Lightweight JavaScript runtime, compiler, REPL, and test runner (STANDARD @aws-sdk bundled)'
arch=('x86_64' 'aarch64')
url='https://github.com/awslabs/llrt'
license=('Apache-2.0')
makedepends=('cmake' 'git' 'llvm-libs>=21.0.0' 'make' 'nodejs' 'parallel' 'rustup' 'zig' 'zstd')
optdepends=(
  'typescript: transpiler for TypeScript code with type checking support'
  'esbuild: fast compiler and bundler for JavaScript and TypeScript'
  'swc-js-bin: drop-in replacement for Babel with compilation and polyfill support'
  'bun-bin: fast runtime, compiler, and bundler for JavaScript and TypeScript'
)
provides=('llrt')
conflicts=('llrt')
options=(!buildflags !makeflags !debug)
source=("git+$url.git")
source_x86_64=('https://github.com/pnpm/pnpm/releases/download/v10.20.0/pnpm-linuxstatic-x64')
source_aarch64=('https://github.com/pnpm/pnpm/releases/download/v10.20.0/pnpm-linuxstatic-arm64')
sha256sums=('SKIP')
sha256sums_x86_64=('2acd94b5f7ba284386243609a46863e1438f8ad4dc1a3b8d16ef5a2c0bbfe30e')
sha256sums_aarch64=('5270159a87dba69a48df112ac833172c1269b6242da478d95245317de981fce7')

_carch="$( [ "$CARCH" == "aarch64" ] && echo "arm64" || echo "x64" )"

prepare() {
  cd llrt

  # Use bsdtar instead of zip
  sed -i "s#zip -j#bsdtar -s ',^.*/,,g' -caf#g" Makefile

  # Use Rust's nightly version from the date of the upstream release to prevent regression issues
  sed -i "s/RUST_VERSION = nightly/RUST_VERSION = $_rust_version/g" Makefile

  # Use pnpm instead of Yarn Classic for faster dependency downloads
  sed -i "s/yarn@1.22.22/pnpm@10.20.0/g" package.json
  echo "nodeLinker: hoisted" > pnpm-workspace.yaml
  local _pnpm="$srcdir/pnpm-linuxstatic-$_carch"
  chmod +x "$_pnpm"

  echo "Downloading..."
  parallel --halt now,fail=1 --line-buffer --link --tagstring '\033[1;{2}m{1}:' '{3} && echo "Done!"' \
    ::: '      Git submodules' '   Rust dependencies' 'AWS SDK dependencies' \
    ::: 33 34 32 \
    ::: 'git submodule update --init --checkout' \
        "rustup toolchain install $_rust_version --target $CARCH-unknown-linux-musl && make stdlib-$_carch && cargo +$_rust_version fetch --target $CARCH-unknown-linux-musl --color never" \
        "$_pnpm install"
}

build() {
  cd llrt
  make "libs-$_carch"
  make "llrt-linux-$_carch$_suffix.zip"
}

package() {
  install -Dm755 "$srcdir/llrt/target/$CARCH-unknown-linux-musl/release/llrt" "$pkgdir/usr/bin/llrt"
  ln -sf "/usr/bin/llrt" "$pkgdir/usr/bin/llrt-$_sdk" # Provide a suffixed alias to llrt
  install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" "$srcdir/llrt/"{LICENSE,THIRD_PARTY_LICENSES,NOTICE}
}
