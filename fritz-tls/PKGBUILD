# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=fritz-tls
pkgver=0.23.0 # renovate: datasource=github-releases depName=tisba/fritz-tls
pkgrel=1
pkgdesc="Automate TLS certificate installation for AVM FRITZ!Box "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/tisba/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('ec392a949ce34333869a2c633aa11bf298027842fd448cf1e249b35efc194e60c94c5126ab56bb81fbe85ef0a88ebe4d6f71042ea96d106db74cb76ebbe8e2ce')
b2sums=('0ffd9263f00db8870297a98fb293f9a018aa95237f33dc567b6cd0fc745aa09301d418a2124d09d7e1915121096e81e49b0b6e74781fe43e5d01cc59eaa70b31')

build() {
  cd "$pkgname-$pkgver"

  # https://wiki.archlinux.org/title/Go_package_guidelines
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"

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
