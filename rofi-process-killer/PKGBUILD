pkgname=rofi-process-killer
pkgver=1.0.0
pkgrel=1
pkgdesc="A rofi module for listing and killing Linux processes with full command line display"
arch=('any')
url="https://github.com/madhur/rofi-process-killer"
license=('MIT')
depends=('rofi' 'procps-ng')
optdepends=('libnotify: desktop notifications for kill status')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('5a590cef291728f774c9f77df9b7136c5b2683999dd496e82c0aebf0cd0b0453')  # Your actual checksum

package() {
    cd "$srcdir/$pkgname-$pkgver"
    
    install -Dm755 rofi-process-killer.sh "$pkgdir/usr/bin/rofi-process-killer"
    install -Dm644 process-killer.rasi "$pkgdir/usr/share/rofi/themes/process-killer.rasi"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 rofi-process-killer.desktop "$pkgdir/usr/share/applications/rofi-process-killer.desktop"
}
