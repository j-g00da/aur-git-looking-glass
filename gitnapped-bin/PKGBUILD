# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=gitnapped
pkgname=$_projectname-bin
pkgver=0.1.4
pkgrel=1
pkgdesc="Find out why you didn’t sleep"
arch=("x86_64")
url="https://github.com/Solexma/gitnapped"
license=("AGPL-3.0-only")
provides=("gitnapped")
conflicts=("gitnapped")
source=("$pkgname-$pkgver.tar.gz::$url/releases/download/v$pkgver/gitnapped-x86_64-unknown-linux-gnu.tar.gz"
        "$_projectname-LICENSE::https://raw.githubusercontent.com/Solexma/$_projectname/refs/tags/v$pkgver/LICENSE"
        "README.md::https://raw.githubusercontent.com/Solexma/$_projectname/refs/tags/v$pkgver/README.md")
sha256sums=('ff7e0b3b94a287820619bfebfd73f7070f698cfa55879627d81b920a7478ecbb'
            '8486a10c4393cee1c25392769ddd3b2d6c242d6ec7928e1414efff7dfb2f07ef'
            '76710d6d9a98dfef43ff7c65a1ee18579cf3447d461e4ba846afc4d0dd9cd8bf')

package() {
    install -Dm 0755 gitnapped "$pkgdir/usr/bin/gitnapped"
    install -Dm 0644 $_projectname-LICENSE "$pkgdir/usr/share/licenses/$_projectname/LICENSE"
    install -Dm 0644 README.md "$pkgdir/usr/share/doc/$_projectname/README.md"
}
