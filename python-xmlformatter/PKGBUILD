# Maintainer: Dani Rodriguez <dani@danirod.es>
# Contributor: Marcell Meszaros < marcell.meszaros AT runbox.eu >
# Contributor: Luis Martinez <luis dot martinez at disroot dot org>
# Contributor: carstene1ns <arch carsten-teibes de> - http://git.io/ctPKG

_distname=xmlformatter
pkgname="python-${_distname}"
pkgver=0.2.8
pkgrel=1
pkgdesc='CLI utility and Python library for formatting XML documents'
arch=('any')
url="https://pypi.org/project/${_distname}"
_repourl="https://github.com/pamoller/${_distname}"
license=('MIT')
depends=('python')
makedepends=('python-build' 'python-installer' 'python-setuptools' 'python-wheel')
checkdepends=('python-pytest')
provides=("${_distname}=${pkgver}")
conflicts=("${_distname}")
source=("${_distname}-${pkgver}.tar.gz::${_repourl}/archive/refs/tags/v${pkgver}.tar.gz")
b2sums=('d20d1917a542dc7d1241a7eeb65437466f89bc74a30cfb0783d998bd0e2f97efecb34a9d50b0681a86485490dfab9cb3f98db59bf315d40ba87b8577e330a34e')

build() {
  cd "${_distname}-$pkgver"
  python -m build --wheel --no-isolation
}

check() {
  cd "${_distname}-$pkgver/test"
  python test_xmlformatter.py
}

package() {
  cd "${_distname}-$pkgver"
  python -m installer --destdir="${pkgdir}/" dist/*.whl

  install -Dm644 README.rst -t "${pkgdir}/usr/share/doc/${pkgname}/"
  local _site="$(python -c 'import site; print(site.getsitepackages()[0])')"
  install -d "${pkgdir}/usr/share/licenses/${pkgname}/"
  ln -s \
    "${_site}/${_distname}-${pkgver}.dist-info/LICENSE.txt" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
