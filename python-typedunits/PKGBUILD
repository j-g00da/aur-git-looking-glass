# Maintainer: Iyán Méndez Veiga <me (at) iyanmv (dot) com>
_pkgname=typedunits
pkgname=python-${_pkgname}
pkgver=0.0.1
pkgrel=1
pkgdesc="A fast units and dimensions library with support for static dimensionality checking and protobuffer serialization"
arch=(x86_64)
url=https://github.com/quantumlib/TypedUnits
license=(Apache-2.0)
depends=(
    cython
    python-attrs
    python-numpy
    python-protobuf
    python-pyparsing
)
makedepends=(
    git
    python-build
    python-installer
    python-setuptools
    python-wheel
)
checkdepends=(python-pytest)
source=($_pkgname::git+https://github.com/quantumlib/TypedUnits#tag=v$pkgver)
b2sums=('05e6c21997fc725dde8b5bcf218c7ad023d49f9ee8ee0954a2e5d22b4125e2be9f3fd3105cac0ef312ecdd8cfba9f6064bfdd2f8dfe32ae1768ed7064f7d3b6d')

build() {
    cd $_pkgname
    python -m build --wheel --no-isolation
}

check() {
    cd $_pkgname
    local python_version=$(python -c 'import sys; print(".".join(map(str, sys.version_info[:2])))')
    python -m installer --destdir=../test_dir dist/*.whl
    rm -rf tunits
    PYTHONPATH="$PWD/../test_dir/usr/lib/python$python_version/site-packages" pytest test
}

package() {
    cd $_pkgname
    python -m installer --destdir="$pkgdir" dist/*.whl
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
