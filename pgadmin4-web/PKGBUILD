pkgname=pgadmin4-web
pkgver=9.11
pkgrel=1
pkgdesc='The web interface for pgAdmin, hosted under Apache HTTPD. pgAdmin is the most popular and feature rich Open Source administration and development platform for PostgreSQL, the most advanced Open Source database in the world.'
arch=('x86_64')
license=('PostgreSQL')
url='https://www.pgadmin.org/'
depends=("pgadmin4-server>=${pkgver}-1" "apache" "mod_wsgi")
makedepends=("syft" "patch" "gcc" "make")
provides=('pgadmin4-web')
source=("pgadmin4-${pkgver}.tar.gz::https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v${pkgver}/source/pgadmin4-${pkgver}.tar.gz" "web.patch")
sha256sums=('8f394156662843440b86a5c73995e14b366d8b0056f69c2aa0b00a3268570a54' 'c1cf92c06d5e6133212be5aeed06cdab60b22745c43a21136c9905c4f0724014')
backup=('etc/httpd/conf/extra/pgadmin4.conf')

prepare() {
  cd "$srcdir/pgadmin4-${pkgver}"
  patch -p1 <"../web.patch"
}

build() {
  cd "$srcdir/pgadmin4-${pkgver}"

  WEBROOT="${srcdir}/pgadmin4-${pkgver}/arch-build/web"

  mkdir -p "${WEBROOT}/usr/pgadmin4/bin/"
  cp "pkg/linux/setup-web.sh" "${WEBROOT}/usr/pgadmin4/bin/"

  syft "${WEBROOT}/" -o cyclonedx-json > "${WEBROOT}/usr/pgadmin4/sbom-web.json"

  mkdir -p "${WEBROOT}/etc/httpd/conf/extra"
  cp "pkg/debian/pgadmin4.conf" "${WEBROOT}/etc/httpd/conf/extra"
}

package() {
  cp -r "${srcdir}/pgadmin4-${pkgver}/arch-build/web/usr"  "${pkgdir}/"
  cp -r "${srcdir}/pgadmin4-${pkgver}/arch-build/web/etc"  "${pkgdir}/"
}
