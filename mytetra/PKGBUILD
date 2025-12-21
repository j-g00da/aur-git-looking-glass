# Maintainer: fft
# Contributor: cyberxndr <cyberxndr@gmail.com>

pkgname=mytetra
pkgver=1.44.183
pkgrel=1
pkgdesc="Personal manager for data memorization and structuring notes"
arch=('x86_64')
url="https://github.com/xintrea/mytetra_dev"
license=('GPL-3.0-only')
depends=('hicolor-icon-theme' 'qt5-base' 'qt5-svg')
source=(
  "https://github.com/xintrea/mytetra_dev/archive/refs/tags/v.${pkgver}.tar.gz"
  'p1.patch'
)

b2sums=(
  'd5c2cfcc462a32572f525a72aea7637101590dc0e6d8e82ce0689c8470121e85ad9ab7774265b572678689e66f80fe10c02efdb5c4ad94bb9d0e7084ec877f22'
  'f86d56aaeb83a5a40f76b219e38352e91860c9dce06afa7bde9cb8342172a5c318f2424160deba48878dd983382a5edcae23178c0e301163ec7a128a85d3ddeb'
)

build(){
  cd "mytetra_dev-v.${pkgver}"
  patch thirdParty/mimetex/mimetex.c ../p1.patch
  sed -i 's/QMAKE_CFLAGS += -DAA/QMAKE_CFLAGS += -DAA -std=gnu17/' thirdParty/mimetex/mimetex.pro
  qmake
  make
}


package(){
  cd "mytetra_dev-v.${pkgver}/app"
  make install INSTALL_ROOT="${pkgdir}"
  mkdir -p "${pkgdir}/usr/bin/"
  mv "${pkgdir}/usr/local/bin/mytetra" "${pkgdir}/usr/bin/"
  rm -r "${pkgdir}/usr/local"
}

