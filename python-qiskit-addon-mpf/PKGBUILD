# Maintainer: Iyán Méndez Veiga <me (at) iyanmv (dot) com>
_name=qiskit-addon-mpf
pkgname=python-${_name}
pkgver=0.3.0
pkgrel=1
pkgdesc="An addon to reduce the Trotter error of Hamiltonian dynamics with multi-product formulas"
arch=(any)
url=https://github.com/Qiskit/qiskit-addon-mpf
license=(Apache-2.0)
depends=(
    python-cvxpy
    python-numpy
    python-qiskit
)
makedepends=(
    python-build
    python-installer
    python-hatchling
)
checkdepends=(
    python-pytest
    python-pytest-subtests
    python-qiskit-addon-utils
)
optdepends=(
    "python-quimb: support for tensor networks"
    "python-qiskit-quimb: simulate circuits using quimb"
    "python-tenpy: simulate strongly correlated quantum systems with tensor networks"
)
source=(
    $_name-$pkgver.tar.gz::https://github.com/Qiskit/$_name/archive/refs/tags/$pkgver.tar.gz
    fix-tests.patch::https://github.com/Qiskit/qiskit-addon-mpf/pull/101.patch
)
b2sums=('707bce8fdf2d3a4bcbab084237697cc0938680ef3de4cc1d5d8c21acc8f040ffae14aa9fc3febc73e9eb7a2a06d340251f78bbd89d869de662937b91b18cfb25'
        'aa4b453b3c0be1425d90ae28560bd1e5871eb25da0c2100b9ee08f5005016f3616825f2621d794b076a2aaf185e0b760dda89dadf6c23787cdda1bc04718bec4')

prepare() {
    patch -Np1 -d $_name-$pkgver < fix-tests.patch
}

build() {
    cd $_name-$pkgver
    python -m build --wheel --no-isolation
}

check() {
    cd $_name-$pkgver
    local python_version=$(python -c 'import sys; print(".".join(map(str, sys.version_info[:2])))')
    python -m installer --destdir=test_dir dist/*.whl
    rm -rf ${_name//-/_}
    PYTHONPATH="$PWD/test_dir/usr/lib/python$python_version/site-packages" pytest test
}

package() {
    cd $_name-$pkgver
    python -m installer --destdir="$pkgdir" dist/*.whl
    install -D -m644 LICENSE.txt "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
