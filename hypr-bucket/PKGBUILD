# Maintainer: Time ON <timeon.haas@gmail.com>
pkgname=hypr-bucket
pkgver=1.0.2
pkgrel=1
pkgdesc="Lightweight and customizable application launcher for Hyprland"
arch=('x86_64' 'aarch64')
url="https://github.com/Time-0N/hypr-bucket"
license=('GPL3')
depends=(
  'gtk4'
  'gtk4-layer-shell'
  'gcc'
  'glibc'
)
makedepends=(
  'cargo'
  'rust'
  'pkgconfig'
)
optdepends=(
  'kitty: Terminal for terminal applications'
  'alacritty: Alternative terminal'
  'wezterm: Alternative terminal'
)
source=("$pkgname-$pkgver.tar.gz::https://github.com/Time-0N/$pkgname/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('SKIP')

prepare() {
  cd "$pkgname-$pkgver"
  export RUSTFLAGS="-C target-cpu=native"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --locked
}

package() {
  cd "$pkgname-$pkgver"

  # Install binary
  install -Dm755 target/release/hbucket "$pkgdir/usr/bin/hbucket"

  # Install CSS resources to config directory
  install -Dm644 resources/default.css "$pkgdir/etc/skel/.config/hyprbucket/default.css"

  # Install desktop file
  install -Dm644 hypr-bucket.desktop "$pkgdir/usr/share/applications/hypr-bucket.desktop" 2>/dev/null || true

  # Install license
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
