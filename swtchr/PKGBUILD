# Maintainer: fk29g <fk29g.uphill912@slmails.com>
pkgname=swtchr
pkgver=0.1.3
pkgrel=1
arch=("x86_64")
pkgdesc="Gnome-style window switcher for the Sway window manager"
url="https://github.com/lostatc/swtchr"
license=("MIT")
depends=("gtk4" "gtk4-layer-shell" "sway")
makedepends=("rust")
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
b2sums=("48d40d68661b31638aca6c79b45ca1805720a7355116f238c0710843f47fc49ca7d5388f9167bbb5d8fe54f1771c9a7ed85d85c8964d5c55187473d8133dda23")

build() {
    cd "$pkgname-$pkgver"
    cargo build --release
}

package() {
    cd "$pkgname-$pkgver"
    install -Dm 0755 target/release/swtchr "$pkgdir/usr/bin/swtchr"
    install -Dm 0755 target/release/swtchrd "$pkgdir/usr/bin/swtchrd"
    install -Dm 0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
