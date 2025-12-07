# Maintainer: bko <aur at bil dot co dot ua>

pkgname=pgadmin4-desktop
pkgver=9.10
pkgrel=2
pkgdesc='The desktop user interface for pgAdmin. pgAdmin is the most popular and feature rich Open Source administration and development platform for PostgreSQL, the most advanced Open Source database in the world.'
arch=('x86_64')
license=('PostgreSQL')
url='https://www.pgadmin.org/'
depends=("pgadmin4-server>=${pkgver}-1" 'xdg-utils' 'python-dbus')
makedepends=("nodejs" "corepack" "npm" "wget" "unzip" "syft")
provides=('pgadmin4-desktop')
source=("pgadmin4-${pkgver}.tar.gz::https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v${pkgver}/source/pgadmin4-${pkgver}.tar.gz")
sha256sums=('479b7b34b25be53b28174d3b688cebf91869204bec75752e06f7de1634c41507')

build() {
  cd "$srcdir/pgadmin4-${pkgver}"

  export COREPACK_HOME="$srcdir/corepack_home"
  mkdir -p "$COREPACK_HOME/bin"
  corepack enable --install-directory "$COREPACK_HOME/bin"
  export PATH="$COREPACK_HOME/bin:$PATH"
  export COREPACK_ENABLE_DOWNLOAD_PROMPT=0
  corepack prepare yarn@stable --activate

  source pkg/linux/build-functions.sh

  _setup_env "${PWD}/pkg/linux/DUMMY" "arch"
  _cleanup "pkg.tar.zst"
  _setup_dirs
  _build_runtime
  syft "${DESKTOPROOT}/" -o cyclonedx-json > "${DESKTOPROOT}/usr/${APP_NAME}/sbom-desktop.json"
}

package() {
  cp -r "${srcdir}/pgadmin4-${pkgver}/arch-build/desktop/usr" "${pkgdir}/"

  # no need to install the license, since pgadmin4-server has already done it
}
