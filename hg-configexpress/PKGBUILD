# Maintainer: Rafaël Kooi <rakooi.foss'youknowthesymbol'gmail.com>
# Contributor: Damien Molinier <damien-43\N{COMMERCIAL AT}gmx.fr>

pkgname=hg-configexpress
pkgver=0.4.0
pkgrel=1
pkgdesc='Mercurial extension to monitor and enforce client configuration from a server'
arch=('any')
license=('GPL-2.0-or-later')
depends=('mercurial')
makedepends=('python-build' 'python-installer' 'python-wheel' 'python-setuptools')
url='https://wiki.mercurial-scm.org/ConfigExpressExtension'
source=("https://files.pythonhosted.org/packages/source/h/${pkgname}/${pkgname}-${pkgver}.tar.gz")
sha512sums=('2cdefd13d4b9b53a2447c93e7813279a437fdbdf2d8ab57bcbd3eb651c91026ff214969d8041def9b276e98827132f8a9ee16e9dd0f5825eb9880b5bd6890e43')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  python -m build --wheel --no-isolation
}

check() {
  # Tests depend on Mercurial sources
  if [[ -n "${HGSRC}" ]]; then
    cd "${srcdir}/${pkgname}-${pkgver}/tests"
    python "${HGSRC}/tests/run-tests.py"
  fi
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  python -m installer --destdir="$pkgdir" dist/*.whl
  rm -f "${pkgdir}/usr/lib/python"*"/site-packages/hgext3rd/"{__pycache__/,}"__init__"*".py"{,o,c}
}

# vim:set ts=2 sw=2 et:
