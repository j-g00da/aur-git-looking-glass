# Maintainer: Mark Collins <tera_1225 hat hotmail.com>
pkgname=matrix-commander
pkgver=8.0.5
pkgrel=1
pkgdesc="Simple CLI-based Matrix client"
arch=('any')
url="https://github.com/8go/matrix-commander"
license=('GPL-3.0-or-later')
makedepends=(
  "python-build"
  "python-installer"
  "python-wheel"
)
depends=(
  "bash"
  "python"
  "python-aiohttp"
  "python-async-timeout" # AUR
  "python-aiofiles"
  "python-emoji"
  "python-markdown"
  "python-matrix-nio" # AUR
  "python-pillow"
  "python-setuptools"
  "python-magic"
  "python-pyxdg"
  "python-atomicwrites"
  "python-cachetools"
  "python-olm"
  "python-peewee"
)
optdepends=(
  "python-notify2: needed for notifications on desktop systems"
)
provides=()
conflicts=()
source=("${pkgname}-${pkgver}::https://files.pythonhosted.org/packages/source/${pkgname::1}/${pkgname}/${pkgname/-/_}-${pkgver}.tar.gz")
sha256sums=('fd1517f037dabd6fc9cbe31952eaa0fd2aa1435aa3118ead2b8898f648647422')

build() {
  cd "${srcdir}/${pkgname/-/_}-${pkgver}"
  python -m build --wheel --no-isolation
}

package() {
  cd "${srcdir}/${pkgname/-/_}-$pkgver"
  python -m installer --destdir="$pkgdir" dist/*.whl
}

