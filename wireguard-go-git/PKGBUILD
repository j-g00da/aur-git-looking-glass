# Contributor: Lex Black <autumn-wind@web.de>
# Contributor: Davide Depau <davide@depau.eu>

_pkgname=wireguard-go
pkgname=${_pkgname}-git
pkgver=0.0.20250522.r0.gf333402
pkgrel=3
pkgdesc="Go userspace implementation of WireGuard"
arch=('i686' 'pentium4' 'x86_64' 'armv7h' 'armv6h' 'aarch64')
url="https://git.zx2c4.com/wireguard-go/"
license=('MIT')
depends=('glibc')
makedepends=('go' 'git')
conflicts=("${_pkgname}")
provides=("${_pkgname}" "wireguard")
source=("${_pkgname}::git+https://git.zx2c4.com/wireguard-go.git"
        "0001-go-guidelines.patch")
sha1sums=('SKIP'
          'e44d694a0db30f5873d4179ac8f80247a16f91b7')


pkgver() {
  cd "$_pkgname"
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "$_pkgname"
  patch -Np2 -i "$srcdir"/0001-go-guidelines.patch
}

build() {
  cd "$_pkgname"
  make DESTDIR="$pkgdir"
}

package() {
  cd "$_pkgname"
  make DESTDIR="$pkgdir" PREFIX=/usr install

  install -vDm644 LICENSE -t "${pkgdir}"/usr/share/licenses/$pkgname/
}
