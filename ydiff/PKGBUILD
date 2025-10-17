# Maintainer: Lex Black <autumn-wind at web dot de>
# Contributor: alejandrogomez <alejandroogomez@gmail.com>

pkgname=ydiff
pkgver=1.4.2
pkgrel=1
pkgdesc="Colored, incremental, side-by-side diff viewer"
arch=('any')
url="http://pypi.python.org/pypi/ydiff/"
license=('BSD-3-Clause')
depends=('python')
makedepends=(python-setuptools python-build python-installer python-wheel)
optdepends=("patchutils: uses filterdiff for context diffs")
conflicts=('cdiff')
source=(${pkgname}-${pkgver}.tar.gz::https://github.com/ymattw/${pkgname}/archive/refs/tags/${pkgver}.tar.gz)
b2sums=('ba1b6b4659d3de7d98c357a0d3c44169d04af9e606aac3ec0ef93512b59e04f5d75846ed19f7392031964f198002ff3192077052351703075b4427bbddc1e51b')


build() {
    cd "$pkgname-$pkgver"
    python -m build --wheel --no-isolation
}

package() {
    cd "$pkgname-$pkgver"
    python -m installer --destdir="$pkgdir" dist/*.whl

    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
