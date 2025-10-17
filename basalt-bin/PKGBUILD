# Maintainer: aik2 <aik2mlj@gmail.com>
#
pkgname=basalt-bin
_name=basalt
pkgver=0.10.3
pkgrel=1
pkgdesc="TUI Application to manage Obsidian vaults and notes directly from the terminal"
arch=('x86_64')
url="https://github.com/erikjuhani/basalt"
license=('MIT')
provides=($_name)
conflicts=($_name)
source=("${url}/releases/download/${_name}%2Fv${pkgver}/${_name}-${pkgver}-x86_64-unknown-linux-gnu.tar.gz")
sha256sums=('b2170d7b3e89f90709590b8d77d33ee91acded937064ecad26a0ae314d1b936f')

package() {
    # Install the binary
    install -Dm755 "$srcdir/target/x86_64-unknown-linux-gnu/release/$_name" "$pkgdir/usr/bin/$_name"
}
