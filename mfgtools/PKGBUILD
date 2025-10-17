# Maintainer: SpieringsAE <maud_spierings@hotmail.com>
# Contributor: Theowhy <aur.theowhy@shizoku.fr>
# Contributor: jpkotta
# Contributor: jona
# Contributor: arti
pkgname=mfgtools
pkgver=1.5.201
pkgrel=4
pkgdesc="Freescale/NXP I.MX Chip image deploy tools"
arch=('x86_64' 'aarch64' 'riscv64')
url="https://github.com/NXPmicro/mfgtools"
license=('BSD-3-Clause')
depends=('bzip2' 'zlib' 'libusb' 'openssl' 'tinyxml2')
makedepends=('cmake')
changelog=History.md
source=(https://github.com/NXPmicro/mfgtools/releases/download/uuu_$pkgver/uuu_source-uuu_$pkgver.tar.gz uuu-complete.bash uuu-cstdint.patch)

sha256sums=('c763b87ffdf10ac5499a0c319463759caa336bc6567b56d6d0ef448590c1a76d'
            'ffc8e32655ce574a4719c85c5c9a3530a5ec619e933fc801a291df8ec506a442'
            'c494ac77183b20b0cae309c8c1ceb19333eb150a0cc8c9e235c085c22ce2ec03')

prepare() {
  patch --directory="uuu-uuu_$pkgver" --forward --strip=1 --input="${srcdir}/uuu-cstdint.patch"
}

build() {
  ls
  cd "uuu-uuu_$pkgver"
  # Remove useless folders to make
  rm -Rf -- bzip2 libusb msvc zlib
  mkdir -p build
  cd build

  cmake -DCMAKE_POLICY_VERSION_MINIMUM=3.5 -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release ..
  make
}

package() {
  cd "uuu-uuu_$pkgver/build"

  make DESTDIR="$pkgdir/" install

  comp_dir="$pkgdir"/etc/bash_completion.d/
  install -d -m 755 "$comp_dir"
  install -m 644 "$srcdir"/uuu-complete.bash "$comp_dir"/uuu-complete.bash

  ./uuu/uuu -udev > 70-uuu.rules
  udev_dir="$pkgdir"/usr/lib/udev/rules.d/
  install -d -m 755 "$udev_dir"
  install -m 644 70-uuu.rules "$udev_dir"/70-uuu.rules

  lic_dir="$pkgdir"/usr/share/licenses/mfgtools/
  install -d -m 755 "$lic_dir"
  install -m 644 ../LICENSE "$lic_dir"/LICENSE
}
