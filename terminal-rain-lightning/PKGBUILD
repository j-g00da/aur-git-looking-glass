# Maintainer: Nihal Kumar <2tv8xupqg at mozmail dot com>
pkgname=terminal-rain-lightning
pkgver=0.1.0
pkgrel=1
pkgdesc="A terminal rain and lightning animation using Python and curses"
arch=('any')
url="https://github.com/rmaake1/terminal-rain-lightning"
license=('MIT')
depends=('python')
makedepends=('git' 'python-pip' 'python-setuptools' 'python-wheel' 'python-build' 'python-installer')
source=("git+https://github.com/rmaake1/terminal-rain-lightning.git")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/terminal-rain-lightning"
  # Extract version from pyproject.toml
  grep '^version' pyproject.toml | head -n1 | cut -d\" -f2
}

prepare() {
  cd "$srcdir/terminal-rain-lightning"
  # Ensure a clean build state if reusing a cache
  rm -rf build dist *.egg-info
}

build() {
  cd "$srcdir/terminal-rain-lightning"
  # Build a wheel via PEP 517
  python -m build --wheel --outdir .
}

package() {
  cd "$srcdir/terminal-rain-lightning"
  # Install into $pkgdir using pip, without pulling external dependencies
  python -m pip install --root="$pkgdir" --no-deps --ignore-installed *.whl
}
