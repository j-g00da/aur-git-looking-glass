# Maintainer: Markus Pesch <markus.pesch plus apps at cryptic.systems>

pkgname=shellyctl
pkgver=0.4.0 # renovate: datasource=github-releases depName=jcodybaker/shellyctl
pkgrel=3
pkgdesc="shellyctl is an unofficial command line client for the Shelly Gen2/3 API. "
arch=('armv7h' 'aarch64' 'x86_64')
url="https://github.com/jcodybaker/$pkgname"
license=('MIT')
makedepends=('go')

source=(
  "$url/archive/refs/tags/v$pkgver.zip"
)
sha512sums=('fd997360d5a1804c642422833c602966acd196dc6668d596b5a1d6eefbd619a54154e5a355b705383900374d284e9eef0066c16d9c997c893bddcd4a30ebd647')
b2sums=('394f831886dd0cf11c8b66feaa0f8a4511a322bdd44eb3cb06794d18b7f215694be00795e96225fe340d945421ec584d6af2afb9fdf1ad1b131d1bd01fc22a55')

build() {
  cd "$pkgname-$pkgver"

  # https://wiki.archlinux.org/title/Go_package_guidelines
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"

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
  install -D --mode 0755 --target-directory "$pkgdir/usr/share/licenses/$pkgname" "$pkgname-$pkgver/LICENSE.md"
}
