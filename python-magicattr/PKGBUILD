# Maintainer: Iyán Méndez Veiga <me (at) iyanmv (dot) com>
_name=magicattr
pkgname=python-$_name
pkgver=0.1.6
pkgrel=1
pkgdesc="A getattr and setattr that works on nested objects, lists and dicts"
arch=(any)
url=https://github.com/frmdstryr/magicattr
license=(MIT)
depends=(python)
makedepends=(
    python-build
    python-installer
    python-setuptools
    python-wheel
)
checkdepends=(python-pytest)
source=($_name-$pkgver.tar.gz::https://github.com/frmdstryr/$_name/archive/refs/tags/v$pkgver.tar.gz)
b2sums=('4ca48fb150b3a49e4649bd0508967582a0b308fc3aa2f4a73961a7c2ab66585d71886fc86d2c291f7ef12477cbc3afaf19c0e34484a41dfa0e81ef395bfe6379')

build() {
    cd $_name-$pkgver
    python -m build --wheel --no-isolation
}

check() {
    cd $_name-$pkgver
    local python_version=$(python -c 'import sys; print(".".join(map(str, sys.version_info[:2])))')
    python -m installer --destdir=../test_dir dist/*.whl
    rm -f magicattr.py
    PYTHONPATH="$PWD/../test_dir/usr/lib/python$python_version/site-packages" pytest tests.py
}

package() {
    cd $_name-$pkgver
    python -m installer --destdir="$pkgdir" dist/*.whl
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
