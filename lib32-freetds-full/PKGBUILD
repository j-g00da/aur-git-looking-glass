_lib32=lib32-
_pkgname=freetds
_pkgname32=$_lib32$_pkgname
pkgname=($_pkgname32-full $_pkgname32-sidebyside64)
pkgver=1.5.8
pkgrel=3
pkgdesc='Library for accessing Sybase and MS SQL Server databases'
url='https://www.freetds.org'
arch=(x86_64)
license=(GPL-2.0-only
         LGPL-2.0-only)
depends=(lib32-glibc
         lib32-krb5
         lib32-openssl
         lib32-readline
         lib32-unixodbc)
provides=($_pkgname32) #both metapackages provide "base" package
source=(https://www.freetds.org/files/stable/$_pkgname-$pkgver.tar.bz2)
sha256sums=('4e7a8afe83e954197084e3d2127be1e37ee9dd5deb0d9e705467e60ec73de4df')

build() {
  cd $_pkgname-$pkgver
  export CFLAGS+=" -m32"
  export CXXFLAGS+=" -m32"

  ./configure \
    --prefix=/usr \
    --libdir=/usr/lib32 \
    --sysconfdir=/etc/freetds \
    --enable-msdblib \
    --enable-krb5 \
    --with-unixodbc=/usr \
    --with-openssl
  make 
}

package_base() {
  cd $_pkgname-$pkgver
  make DESTDIR="$pkgdir" install
}

package_lib32-freetds-sidebyside64() {
  conflicts+=(lib32-freetds-full)

  package_base

  #generate a minimal install with no etc, docs or man, so that it can live alongside main `freetds` package
  rm -rf $pkgdir/etc/
  rm -rf $pkgdir/usr/share
  rm -rf $pkgdir/usr/include
  for f in $pkgdir/usr/bin/*; do
    mv -v $f ${f}32
  done
}

package_lib32-freetds-full() {
  conflicts+=(freetds
              lib32-freetds-sidebyside64)
  backup+=(etc/freetds/freetds.conf
           etc/freetds/locales.conf
           etc/freetds/pool.conf)

  package_base
}
