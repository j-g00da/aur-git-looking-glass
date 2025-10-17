# Maintainer: Soymadip <soumadip@zohomail.in>

pkgname=mpv-mpris2-bin
pkgver=0.0.6
pkgrel=1
pkgdesc="Rust implementation of the MPRIS v2 DBus interface for the mpv."
arch=('x86_64')
url="https://github.com/eNV25/mpv-mpris2"
license=('MIT-0')
depends=('mpv')
conflicts=('mpv-mpris' 'mpv-mpris-git')
source=("${url}/releases/download/v${pkgver}/mpris-${arch}-unknown-linux-gnu.so")
sha256sums=('c3bce3c8c59c1d2e8f42397fdea209b8e044812bfbdd3a17108f66205070eee2')

package() {
  install -D -m 644 mpris-x86_64-unknown-linux-gnu.so "$pkgdir/etc/mpv/scripts/mpris.so"
}
