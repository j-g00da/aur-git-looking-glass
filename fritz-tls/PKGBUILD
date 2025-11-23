# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=fritz-tls
pkgver=0.25.0 # renovate: datasource=github-releases depName=tisba/fritz-tls
pkgrel=1
pkgdesc="Automate TLS certificate installation for AVM FRITZ!Box "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/tisba/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  ${pkgname}-v${pkgver}.zip::"$url/archive/refs/tags/v${pkgver}.zip"
)
sha512sums=('59140b9dda23230d30e78e38dda389c1574930d490ef23dd767fcaff0cdc790d6886ad24735c8bea870b436363abdbc93235f7d4fc84299bb560d9acc58e4968')
b2sums=('d7b16af7e7c5baffad12b0574be82181232b1aa58a82dca0832b128f6065965bd3e40fd399a90c77b500c5509e192a49f9b41a806a8cffbe7a2617d5bd3f4d98')

prepare() {
  cd ${pkgname}-${pkgver}

  export GONOSUMDB="${GONOSUMDB}"
  export GOPATH="${srcdir}"
  export GOPROXY="${GOPROXY}"

  env | sort | grep -E '^C?GO'

  go mod download -modcacherw
}

build() {
  cd "$pkgname-$pkgver"

  # https://wiki.archlinux.org/title/Go_package_guidelines
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"

  export GONOSUMDB="${GONOSUMDB}"
  export GOPATH="${srcdir}"
  export GOPROXY="${GOPROXY}"

  env | sort | grep -E '^C?GO'

  go build -v \
    -trimpath \
    -buildmode=pie \
    -mod=readonly \
    -modcacherw \
    -ldflags "-linkmode external -extldflags \"${LDFLAGS}\"" \
    -o $pkgname \
    .
}

package() {
  # binary
  install -D --mode 0755 --target-directory "$pkgdir/usr/bin" "$pkgname-$pkgver/$pkgname"

  # license
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE"
}
