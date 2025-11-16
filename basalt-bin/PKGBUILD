# Maintainer: aik2 <aik2mlj@gmail.com>
#
pkgname=basalt-bin
_name=basalt
pkgver=0.10.4
pkgrel=1
pkgdesc="TUI Application to manage Obsidian vaults and notes directly from the terminal"
arch=('x86_64')
url="https://github.com/erikjuhani/basalt"
license=('MIT')
provides=($_name)
conflicts=($_name)
source=("${url}/releases/download/${_name}%2Fv${pkgver}/${_name}-${pkgver}-x86_64-unknown-linux-gnu.tar.gz")
sha256sums=('64d8fe9c6eb4c2fd353afd4bd909eb3cbbf6eafa4c513c0f861e972ee8f5e7aa')

package() {
    # Install the binary
    install -Dm755 "$srcdir/target/x86_64-unknown-linux-gnu/release/$_name" "$pkgdir/usr/bin/$_name"
}
