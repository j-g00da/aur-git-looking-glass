# Maintainer: Andy Flesner <andy at flesner dot com>
# Contributor: Kenneth Stier <kenny at millhousen dot tech>

pkgname=rollo-printer
pkgver=1.8.4
pkgrel=1
pkgdesc='Rollo Thermal Printer Driver for Linux'
arch=('x86_64')
url='https://www.rollo.com/driver-linux/'
license=('GPL3')
depends=('cups')
makedepends=('gcc' 'make')
source=("https://rollo-main.b-cdn.net/driver-dl/linux/rollo-cups-driver-${pkgver}.tar.gz"
        "https://rollo-main.b-cdn.net/driver-dl/linux/rollo-cups-driver-${pkgver}.tar.gz.sig")
sha512sums=('6a7bbdcc6ba0bfa423de34d51e525270f1961977adfb82d7a6180713eff2200e7cc1814c58039272a78d1f37f4343df4ff52324f728966c6505f621a35a1b7e9'
            'SKIP')
validpgpkeys=('B97479172D7D70EF193B2B2FE3ACFF5DAFB03654')


build() {
  cd "${srcdir}/rollo-cups-driver-${pkgver}"
  
  # Configure the build
  ./configure --prefix=/usr

  # Build the driver
  make
}

package() {
  cd "${srcdir}/rollo-cups-driver-${pkgver}"
  
  # Install the driver
  make DESTDIR="${pkgdir}" install
}
