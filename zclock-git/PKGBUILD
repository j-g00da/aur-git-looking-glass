# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=zclock
pkgname=$_projectname-git
pkgrel=1
pkgver=r4.cf8403a
pkgdesc="A cross-platform terminal digital clock"
arch=("x86_64")
url="https://github.com/tr1ckydev/zclock"
license=('MIT')
makedepends=("zig>=0.14" "git")
source=(git+$url.git)
sha256sums=("SKIP")

pkgver() {
    cd $_projectname
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cd $_projectname
    zig build -Doptimize=ReleaseFast
}

package() {
    cd $_projectname
    install -Dm 755 zig-out/bin/zclock "$pkgdir/usr/bin/zclock"
    install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$_projectname/LICENSE"
    install -Dm 644 README.md "$pkgdir/usr/share/doc/$_projectname/README.md"
}
