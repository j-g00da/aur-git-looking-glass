# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=clidle
pkgname=$_projectname-bin
pkgver=0.1.0
pkgrel=1
pkgdesc="Play Wordle from your terminal"
arch=("x86_64")
url="https://github.com/ajeetdsouza/clidle"
license=("MIT")
makedepends=("go")
provides=("clidle")
conflicts=("clidle")
source=("$pkgname-$pkgver.tar.gz::$url/releases/download/v$pkgver/clidle_Linux_x86_64.tar.gz")
b2sums=("ec185142afb4a8cad523881a7db0c2cdcdf2a5e97d38d5662b2eb5cbeb32721bd7b80d6c7fdd67c62e973b0e5c2a9638ddeb36ecf8cf752cdd4791bbf90f3aa6")

package() {
    install -Dm 0755 clidle "$pkgdir/usr/bin/clidle"
    install -Dm 0644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
