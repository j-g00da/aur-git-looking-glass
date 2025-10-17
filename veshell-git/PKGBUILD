# Maintainer: PapyElGringo <adrien@pesler.be>
pkgname=veshell-git
pkgver=alpha.1.r138.g04fce58
pkgrel=1
pkgdesc="An innovative not-desktop environment for Linux made with modern technologies like Flutter and Rust."
arch=('x86_64' 'aarch64')
url="https://github.com/free-explorers/veshell"
license=('GPL3')
depends=(
  'fontconfig'
  'libseat.so'
  'libinput'
  'libxcb'
  'libxkbcommon'
  'mesa'
  'pixman'
  'systemd'
  'wayland'
)
makedepends=(
  'cargo'
  'git'
  'clang'
)
provides=('veshell')
conflicts=('veshell')
source=("git+https://github.com/free-explorers/veshell.git")
sha256sums=('SKIP')

pkgver() {
  cd "${pkgname%-git}"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  export CARGO_HOME="${srcdir}/${pkgname%-git}/.cargo"
  export CARGO_TARGET_DIR=target

  # Tell build.rs to link against system-installed shared libs
  export VESHELL_LIB_DIR="/usr/lib/veshell"

  cd "${pkgname%-git}"
  cargo build --release
}

package() {
  cd "${pkgname%-git}"

  # Install binaries and system files
  install -Dm755 target/release/veshell                        -t "${pkgdir}/usr/bin/"
  install -Dm755 extra/assets/veshell-session                  -t "${pkgdir}/usr/bin/"
  install -Dm644 extra/assets/veshell.desktop                  -t "${pkgdir}/usr/share/wayland-sessions/"
  install -Dm644 extra/assets/veshell-portals.conf             -t "${pkgdir}/usr/share/xdg-desktop-portal/"
  install -Dm644 extra/assets/veshell-shutdown.target          -t "${pkgdir}/usr/lib/systemd/user/"

  # Install systemd service file
  install -Dm644 <(sed "s|@bindir@|/usr/bin|" extra/assets/veshell.service.in) \
  "${pkgdir}/usr/lib/systemd/user/veshell.service"

  # Install Flutter engine
  install -Dm644 extra/third_party/flutter_engine/release/libflutter_engine.so -t "${pkgdir}/usr/lib/veshell/"

  # Determine architecture-specific paths
  local arch="x64"
  [[ "$CARCH" == "aarch64" ]] && arch="arm64"

  # Install app library
  install -Dm644 "src/shell/build/linux/${arch}/release/bundle/lib/libapp.so" -t "${pkgdir}/usr/lib/veshell/"

  # Install flutter_assets data directory
  install -d -m755 "${pkgdir}/usr/share/veshell/data"
  cp -r "src/shell/build/linux/${arch}/release/bundle/data/"* "${pkgdir}/usr/share/veshell/data/"

  # install settings directory if present
  install -d -m755 "${pkgdir}/usr/share/veshell/settings"
  cp -r extra/settings/* "${pkgdir}/usr/share/veshell/settings/"
  
}
