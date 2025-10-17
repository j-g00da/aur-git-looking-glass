# Maintainer: Silvan Gümüsdere <silvan@trollbox.org>

pkgname=python-opensearch
_name=opensearch-py
_alt_name=opensearch_py
pkgver=3.0.0
pkgrel=1
pkgdesc='Python Client for OpenSearch'
arch=('any')
url='https://github.com/opensearch-project/opensearch-py'
license=('Apache-2.0')
depends=('python-urllib3' 'python-requests' 'python-dateutil' 'python-certifi' 'python-events')
makedepends=('python-setuptools')
source=("https://files.pythonhosted.org/packages/source/${_name::1}/${_name}/${_alt_name}-${pkgver}.tar.gz")
sha256sums=('ebb38f303f8a3f794db816196315bcddad880be0dc75094e3334bc271db2ed39')

build() {
    cd "${_alt_name}-${pkgver}"
    python setup.py build
}

package() {
    cd "${_alt_name}-${pkgver}"
    python setup.py install --root="${pkgdir}" --optimize=1
}

