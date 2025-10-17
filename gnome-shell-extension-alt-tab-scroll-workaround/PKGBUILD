# Maintainer: Łukasz Moroz <lukaszmoroz@gmail.com>

pkgname=gnome-shell-extension-alt-tab-scroll-workaround
pkgver=9
pkgrel=1
pkgdesc="Temporary fix for a bug that buffers the scroll between different windows (e.g., Chrome and VS Code)"
arch=('any')
url="https://github.com/lucasresck/gnome-shell-extension-alt-tab-scroll-workaround"
license=('GPL3')
depends=('gnome-shell')
source=("$pkgname-$pkgver.tar.gz::https://github.com/lucasresck/gnome-shell-extension-alt-tab-scroll-workaround/archive/refs/tags/v$pkgver.tar.gz")
sha512sums=('e34fd619d5058bc92e671d5e33d9045a46d4a10dd1d5189de6478487ae8a8e2a8ead0ac135a73e5eaf186704e1d5d4b01fe6d52d65c0dff7d2a19eb0fd9dcb3d')

package() {
    cd "$pkgname-$pkgver"
    _uuid='alt-tab-scroll-workaround@lucasresck.github.io'
    install -Dm644 -t "$pkgdir/usr/share/gnome-shell/extensions/$_uuid" extension.js metadata.json
}
