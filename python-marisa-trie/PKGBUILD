# Maintainer:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: Mark E.A. <evalapply ``dot'' aur ``at'' airmail ``dot'' cc>

pkgname=python-marisa-trie
_pyname=marisa_trie
pkgver=1.3.1
pkgrel=1
pkgdesc='Static memory-efficient & fast Trie-like structures for Python (based on marisa-trie C++ library)'
arch=('any')
url="https://github.com/pytries/marisa-trie"
license=('MIT')
depends=('python')
makedepends=('cython' 'python-pip' 'python-setuptools' 'python-wheel')
source=("https://files.pythonhosted.org/packages/c5/e3/c9066e74076b90f9701ccd23d6a0b8c1d583feefdec576dc3e1bb093c50d/${_pyname}-${pkgver}.tar.gz")
sha256sums=('97107fd12f30e4f8fea97790343a2d2d9a79d93697fe14e1b6f6363c984ff85b')

build() {
  cd "${_pyname}-${pkgver}"

  python setup.py build
}

package() {
  cd "${_pyname}-${pkgver}"

  python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
