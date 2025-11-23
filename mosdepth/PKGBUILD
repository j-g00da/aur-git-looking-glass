# Maintainer: Michał Wojdyła < micwoj9292 at gmail dot com >
# Contributor:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: Clint Valentine <valentine.clint@gmail.com>

pkgname=mosdepth
pkgver=0.3.12
pkgrel=1
pkgdesc='Fast BAM/CRAM depth calculation for WGS, exome, or targeted sequencing'
arch=('x86_64')
url="https://github.com/brentp/${pkgname}"
license=('MIT')
depends=('htslib')
makedepends=('git' 'nim')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz")
sha256sums=('8047865fb446b7b4da3dc11226febf00e8dfdaf4e203972a53aeb5fb037bdb4d')

build() {
  cd "${pkgname}-${pkgver}"
  nimble build -y --passC:-Wno-error=incompatible-pointer-types
}

package() {
  cd "${pkgname}-${pkgver}"

  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -Dm755 "${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
}
