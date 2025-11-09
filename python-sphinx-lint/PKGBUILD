# Maintainer: Luc Khai Hai <lkh42t@gmail.com>

pkgname=python-sphinx-lint
_name=${pkgname#python-}
pkgver=1.0.1
pkgrel=2
pkgdesc='Check for stylistic and formal issues in .rst and .py files included in the documentation.'
arch=('any')
url=https://github.com/sphinx-contrib/sphinx-lint
license=('PSF-2.0')
depends=('python' 'python-regex'
         # AUR
         'python-polib')
makedepends=('git' 'python-build' 'python-hatch-vcs' 'python-hatchling' 'python-installer')
source=("$pkgname::git+$url#tag=v$pkgver")
b2sums=('0f7c66abf45fa5f992c6b7b015200450556c7b52730d9c0c5a1e50f019dc779ad58d95e6a4c90a8754477feee986bb9e7ec966d4cc4b00ee444f3a662d46ccad')

build() {
  cd "$pkgname"
  python -m build --wheel --no-isolation
}

package() {
  cd "$pkgname"
  python -m installer --destdir="${pkgdir}" dist/*.whl
}

# vi: sts=2 sw=2 et
