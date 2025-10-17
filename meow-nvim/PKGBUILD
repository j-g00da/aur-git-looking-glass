# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=meow
pkgname=$_projectname-nvim
pkgver=1.0.2
pkgrel=2
pkgdesc="cat alternative using Neovim for highlighting and configuration"
arch=("x86_64")
url="https://github.com/datsfilipe/$_projectname"
license=("MIT")
depends=("neovim")
makedepends=("rust")
source=("$_projectname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
b2sums=('4461283b68a79cb77c5df043102a10a97f78d04a63436c67d195411925bce95a1c255e33a04b7a2a22de48a686ac4958a6d2caea1e7796ac48fb1bf9585028a0')

build() {
    cd "$_projectname-$pkgver"
    cargo build --release
}

package() {
    cd "$_projectname-$pkgver"
    install -Dm 0755 target/release/meow "$pkgdir/usr/bin/meow"
    install -Dm 0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
