# Maintainer: Esk <esk@esk.lol>

pkgname=pgcat
pkgver=1.2.0
pkgrel=2
pkgdesc="PostgreSQL pooler with sharding, load balancing and failover support."
arch=('x86_64')
url="https://github.com/postgresml/pgcat"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=(
  "$pkgname-$pkgver.tar.gz::https://github.com/postgresml/$pkgname/archive/refs/tags/v$pkgver.tar.gz"
)
sha512sums=('c8aeeaa0cb9125e8e5cd541421e2478560b740353337d13e5f4b5896ba044b683006272f72a5fb65649f1ef286d1c837103f503b9e1826c35f3dbeeeffa886cd')
options=(!lto)
backup=(
    'etc/pgcat.toml'
    'usr/lib/systemd/system/pgcat.service'
)

build() {
  cd "$pkgname-$pkgver"

  cargo build --release --locked
}

package() {
  cd "$pkgname-$pkgver"

  install -Dm755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm640 "pgcat.minimal.toml" "$pkgdir/etc/pgcat.toml"
  install -Dm644 "README.md" "$pkgdir/usr/share/doc/${pkgname}/README.md"
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/${pkgname}/LICENSE-MIT"
  install -Dm644 "pgcat.service" "$pkgdir/usr/lib/systemd/system/pgcat.service"
}
