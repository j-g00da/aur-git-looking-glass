# Maintainer: Silvan Gümüsdere <silvan@trollbox.org>

pkgname=python-opensearch
_name=opensearch-py
_alt_name=opensearch_py
pkgver=3.1.0
pkgrel=1
pkgdesc='Python Client for OpenSearch'
arch=('any')
url='https://github.com/opensearch-project/opensearch-py'
license=('Apache-2.0')
depends=('python-urllib3' 'python-requests' 'python-dateutil' 'python-certifi' 'python-events')
makedepends=('python-setuptools')
source=("${pkgname}-${pkgver}.tar.gz::https://files.pythonhosted.org/packages/source/${_name::1}/${_name}/${_alt_name}-${pkgver}.tar.gz")
sha256sums=('883573af13175ff102b61c80b77934a9e937bdcc40cda2b92051ad53336bc055')

build() {
    cd "${_alt_name}-${pkgver}"
    python setup.py build
}

package() {
    cd "${_alt_name}-${pkgver}"
    python setup.py install --root="${pkgdir}" --optimize=1
}

