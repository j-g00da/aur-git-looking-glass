# Maintainer: BlackFuffey ethanthecomputerman@gmail.com

pkgname=cd-memo
pkgver=2024.11.v4
pkgrel=6
pkgdesc="Enhanced cd that memorizes your working directory across sessions"
arch=('any')
url="https://github.com/BlackFuffey/cd-memo"
license=('MIT')
depends=('bash')
source=("cd-memo" "cd-memo-init" "cd-memo-init-ns" "README.md" "LICENSE")

package() {
    install -Dm755 "$srcdir/cd-memo" "$pkgdir/usr/bin/cd-memo"
    install -Dm755 "$srcdir/cd-memo-init" "$pkgdir/usr/bin/cd-memo-init"
    install -Dm755 "$srcdir/cd-memo-init-ns" "$pkgdir/usr/bin/cd-memo-init-ns"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

sha256sums=('950c3d8ffd1392cd19a762889aeb760e68997eef58ba6617348b5439e3547cb4'
            'ed2d94af03408f8d50f5d8d658cb1870acdb16f9e1cffd9bccc59e9f319dee2a'
            'a6f6fb02110155313dcc2afb3613e199abe812ead940bb0376f525822fa6896e'
            '8e648b8f9671e4cd6126323392e0eaede6da4a2e73bc79e1b8bbce316c995273'
            'b8c42f6ef4fa7552a40d029fa9e58eadf12090642febb21db1b47a13cca09f01')
