# Maintainer: 7Ji <pugokughin@gmail.com>

_pkgbase=snasync
_srcname="${_pkgbase}"
pkgname=${_pkgbase}-git
pkgver=0.1.0.r16.c996e7f
pkgrel=1
pkgdesc="A simple and naive Bash script to sync Btrfs snapshots created by snapper from hot storage to cold and/or remote storage"
arch=('any')
url="https://github.com/7Ji/${_srcname}"
license=('AGPL-3.0-or-later')
depends=('btrfs-progs')
optdepends=('openssh: remote sync')
conflicts=("${_pkgbase}")
provides=("${_pkgbase}=${pkgver}")
source=(
  "${_srcname}::git+https://github.com/7Ji/${_pkgbase}.git"
)
sha256sums=(
  'SKIP'
)

pkgver() {
  printf "%s" "$(git --git-dir "${_srcname}/.git" describe --tags | sed 's/^v//;s/\([^-]*-\)g/r\1/;s/-/./g')"
}

package() {
  backup=('etc/conf.d/snasync')
  cd "${_srcname}"
  make install DESTDIR="${pkgdir}" INTEGRATION=systemd
}
