# Maintainer: Silvan Gümüsdere <silvan@trollbox.org>

pkgname=gauth
pkgver=1.5.0
pkgrel=2
pkgdesc="Two-factor authentication (2FA) in the terminal"
arch=('x86_64')
url="https://github.com/pcarrier/gauth"
license=('ISC')
makedepends=('go')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('5c98287f5c209b9f02ec62ede4abd4117aa3ca738fbcb4153a6ec1e966f492a8')

prepare(){
  cd "${pkgname}-${pkgver}"
  export GOPATH="${srcdir}"
  mkdir -p build/
}


build() {
  cd "${pkgname}-${pkgver}"
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"
  go build -o build
}

package() {
  cd "${pkgname}-${pkgver}"
  install -Dm755 build/${pkgname} "${pkgdir}"/usr/bin/${pkgname}
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}

