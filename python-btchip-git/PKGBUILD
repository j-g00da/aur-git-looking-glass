# Maintainer:  Maximilian Weiss <$(echo "bWF4QG1heHdlaXNzLmlv" | base64 -d)>
# Contributor: Timothy Redaelli <timothy.redaelli@gmail.com>
# Contributor: Andy Weidenbaum <archbaum@gmail.com>

pkgname=python-btchip-git
pkgver=0.1.32
pkgrel=9
pkgdesc="Python library to communicate with BTChip dongle"
arch=('any')
depends=('python-hidapi' 'libusb-compat' 'libusb' 'libsystemd')
makedepends=('python-setuptools' 'patch')
optdepends=('btchip-udev: access BTChip as non-root user' 'python-pyscard: for smartcard support')
url="https://github.com/LedgerHQ/btchip-python"
license=('Apache-2.0')
provides=('python-btchip-git' 'python-btchip')
conflicts=('python-btchip-git' 'python-btchip')
source=('git+https://github.com/LedgerHQ/btchip-python' 'python-btchip-0.1.32-setup.patch')
sha256sums=('SKIP'
            '64aea33f1234b6a6c0e7f9e8bb8b4fb6156c118b585ef0f4398809303e391c89')

pkgver() {
    cd "$srcdir/btchip-python/"
    git tag -l | sed 's/v//g' | sort | tail -n 1
}

build() {
  cd "$srcdir/btchip-python/"
  git checkout $(git tag -l | sed 's/v//g' | sort | tail -n 1) > /dev/null 2>&1
  patch -Np1 -i "../../python-btchip-0.1.32-setup.patch"
  python setup.py build
}

package() {
  cd "$srcdir/btchip-python/"
  python setup.py install --root="$pkgdir" --optimize=1
}