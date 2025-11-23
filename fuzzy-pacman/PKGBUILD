pkgname=fuzzy-pacman
pkgver=2.0.0
pkgrel=1
pkgdesc="Fuzzy pacman wrapper using skim (sk). Provides interactive package and system management via subcommands."
arch=('any')
url="https://github.com/brunos3d/fuzzy-pacman"
license=('MIT')
depends=('bash' 'pacman' 'skim' 'systemd')
optdepends=('git: improves some file lookup operations')
source=("fpm" "fpm.1")
sha256sums=('SKIP' 'SKIP')

package() {
  install -Dm755 "$srcdir/fpm" "$pkgdir/usr/bin/fpm"

  # install manpage
  install -Dm644 "$srcdir/fpm.1" "$pkgdir/usr/share/man/man1/fpm.1"
  gzip -f "$pkgdir/usr/share/man/man1/fpm.1"
}
