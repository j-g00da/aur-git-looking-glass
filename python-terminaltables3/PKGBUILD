# Maintainer: Andrew O'Neill <andrew at haunted dot sh>

pkgname=python-terminaltables3
_pyname=terminaltables3
pkgver=4.0.0
pkgrel=1
pkgdesc="Easily draw tables in terminal/console applications from a list of lists of strings"
arch=('any')
url="https://github.com/matthewdeanmartin/${_pyname}"
license=('MIT')
depends=('python')
makedepends=('python-build' 'python-installer' 'python-poetry-core')
checkdepends=('python-pytest' 'python-colorama' 'python-termcolor' 'python-colorclass')
source=("${_pyname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz")
sha256sums=('44df92e82b45fadf4e6af8e3a77214cce455a4e1ee66c3f8c871988e1f58f776')

build() {
  cd "${_pyname}-${pkgver}"

  python -m build --wheel --no-isolation
}

check() {
  cd "${_pyname}-${pkgver}"

  FORCE_COLOR=1 pytest
}

package() {
  cd "${_pyname}-${pkgver}"

  python -m installer --destdir="${pkgdir}" --compile-bytecode=2 dist/*.whl
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 example*.py -t "${pkgdir}/usr/share/doc/${pkgname}/examples"
}
