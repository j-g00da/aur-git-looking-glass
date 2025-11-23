# Maintainer: bko <aur at bil dot co dot ua>

pkgname=pgadmin4-desktop
pkgver=9.10.1
_realver=9.10-1.plucky
pkgrel=1
pkgdesc='The desktop user interface for pgAdmin. pgAdmin is the most popular and feature rich Open Source administration and development platform for PostgreSQL, the most advanced Open Source database in the world.'
arch=('x86_64')
license=('PostgreSQL')
url='https://www.pgadmin.org/'
depends=("pgadmin4-server" 'xdg-utils' 'python-dbus')
provides=('pgadmin4-desktop')
source=(${pkgname}-${pkgver}-x86_64.deb::"https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/plucky/dists/pgadmin4/main/binary-amd64/${pkgname}_${_realver}_amd64.deb")
sha256sums=('1fc103aaf1e7dd2ea73d9fc93b4354df0a054441ae7a72343f9dca43d1a5d622')

package() {
  # Extract package data
  tar -x --zstd -f data.tar.zst -C "${pkgdir}"
}
