# Maintainer: asm0dey <pavel.finkelshtein@gmail.com>

pkgname=fselect
pkgver=0.9.0
pkgrel=1
arch=('i686' 'x86_64')
url="https://github.com/jhspetersson/fselect"
license=("MIT")

pkgdesc='Find files with SQL-like queries'

source=("$pkgver.tar.gz::https://github.com/jhspetersson/$pkgname/archive/$pkgver.tar.gz")
sha512sums=('4f2afb6c346ccdeea790497e2085f2026eb6084ebb76cc58083ad2e84a7e6b2dc5b462bd7df4846576ca73051b1a258589025998dd767535bebc32a7e18b4c83')
makedepends=('rust' 'cmake')
depends=('gcc-libs')
conflicts=('fselect-git')
provides=('fselect')
options=('!lto')

build() {
    cd "$pkgname-$pkgver"
    cargo build --release
}

package() {
    gzip "$srcdir/fselect-$pkgver/docs/fselect.1"
    install -Dm644 "$srcdir/fselect-$pkgver/docs/fselect.1.gz" "$pkgdir/usr/share/man/man1/fselect.1.gz"
    install -Dm755 "$pkgname-$pkgver/target/release/fselect" "$pkgdir/usr/bin/fselect"
    install -Dm644 "$pkgname-$pkgver/LICENSE-MIT" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    rm -f "$srcdir/fselect-$pkgver/docs/fselect.1.gz"
}
