# Maintainer: Ash Hellwig <ahellwig.dev@gmail.com>
# Contributor: Ash Hellwig <ahellwig.dev@gmail.com>
pkgname=ttf-materialicons-regular-for-inline
pkgver=0.1.0
pkgrel=1
pkgdesc='A patched material icons font required for using the material icon set for i3status-rust.'
arch=('any')
url="https://github.com/ashellwig/ttf-materialicons-regular-for-inline"
license=('Apache-2.0')
source=(
    "MaterialIcons-Regular-for-inline.ttf"
    "LICENSE"
)
sha256sums=(
    '86ecbf127d185fa6e4266ac36b3c4f96db1664e50fc46b90b35dabe8bfa1fa80'
    '58d1e17ffe5109a7ae296caafcadfdbe6a7d176f0bc4ab01e12a689b0499d8bd'
)
md5sums=(
    'b60070d838a44f1e52a276609a605e8a'
    '175792518e4ac015ab6696d16c4f607e'
)

package() {
    install -dm 755 "${pkgdir}/usr/share/fonts/TTF"
    install -m 644 MaterialIcons-Regular-for-inline.ttf "${pkgdir}/usr/share/fonts/TTF/"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
