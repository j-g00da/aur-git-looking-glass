pkgname=dualsensectl
pkgver=0.7
pkgrel=1
pkgdesc='Tool for controlling Sony PlayStation 5 DualSense controller on Linux'
arch=('x86_64')
conflicts=('dualsensectl-git')
url='https://github.com/nowrep/dualsensectl'
license=('GPL2')
depends=('dbus' 'hidapi')
makedepends=('make' 'gcc')
source=("$pkgname-$pkgver.tar.gz::https://github.com/nowrep/dualsensectl/archive/refs/tags/v${pkgver}.tar.gz")
sha512sums=('d04b12c004f2f92134b04c2b6495f4b12d51c75c237a9a5f0df7733e013b4623ccb229f3f1be4037b0a5f5cadaf72285e6665313fcfbb3e5cee044fc440da020')

build() {
    cd "$pkgname-$pkgver"
    arch-meson build
    meson compile -C build
}

package() {
    cd "$pkgname-$pkgver"
    meson install -C build --destdir "$pkgdir"
    install -D -m 755 -p completion/dualsensectl $pkgdir/usr/share/bash-completion/completions/dualsensectl
    install -D -m 755 -p completion/_dualsensectl $pkgdir/usr/share/zsh/site-functions/_dualsensectl
}
