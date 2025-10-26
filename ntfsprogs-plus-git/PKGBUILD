# AUR Maintainer: Shadichy <shadichy@blisslabs.org>

_pkgname=ntfsprogs-plus
pkgname=${_pkgname}-git

_repo=ntfsprogs-plus/ntfsprogs-plus
url="https://github.com/${_repo}"

pkgver=0.9.15+2+g9cd9891
pkgrel=1

pkgdesc='NTFS filesystem driver and utilities'
arch=('x86_64')
license=('GPL-2.0-or-later')
depends=('util-linux')
makedepends=(
  'git'
  'jq'
  'autoconf'
  'automake'
  'libtool'
  'libgcrypt'
  'pkgconf'
)
conflicts=('ntfsprogs' 'ntfs-3g' 'ntfsprogs-plus')
replaces=('ntfsprogs' 'ntfs-3g' 'ntfsprogs-plus')
provides=('ntfsprogs')

source=("${_pkgname}::git+${url}.git")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${_pkgname}"
  git describe --long --tags | sed 's#v##;s#-RC#.rc#;s#-#+#g'
}

prepare() {
  cd ${srcdir}/${_pkgname}
  ./autogen.sh
}

build() {
  cd ${srcdir}/${_pkgname}
  ./configure \
    --prefix=/usr \
    --sbin=/usr/bin \
    --includedir=/usr/include/ntfsprogs-plus \
    --mandir=/usr/share/man \
    --disable-ldconfig \
    --enable-xattr-mappings \
    --enable-posix-acls \
    --enable-extras \
    --enable-crypto

  make
}

package() {
  cd ${srcdir}/${_pkgname}
  make DESTDIR="${pkgdir}" rootbindir=/usr/bin rootsbindir=/usr/bin rootlibdir=/usr/lib install

  # License
  install -dm644 "${pkgdir}/usr/share/licenses/${_pkgname}"
  install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
}
