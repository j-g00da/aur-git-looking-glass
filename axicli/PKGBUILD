# PKGBUILD
# Maintainer: Bernardo Kuri <aur+axicli@bkuri.com>

pkgname=axicli
pkgver=3.9.6
pkgrel=2
pkgdesc="AxiDraw CLI and Python API for controlling AxiDraw pen plotters (bundles plotink & ink_extensions)"
url="https://axidraw.com/doc/cli_api"
arch=('any')
license=('custom')
install=axicli.install

# Vendor these versions from PyPI (adjust as desired)
_pink_ver=1.9.0
_inkext_ver=2.0.0

depends=(
  'python>=3.8'
  'python-lxml'
  'python-pyserial'
  'python-requests'
)
makedepends=(
  'python-build'
  'python-installer'
  'unzip'
)
optdepends=(
  'python-numpy: enhanced math operations'
  'python-pillow: image processing'
)

source=(
  'https://cdn.evilmadscientist.com/dl/ad/public/AxiDraw_API.zip'
  "https://files.pythonhosted.org/packages/source/p/plotink/plotink-${_pink_ver}.tar.gz"
  "https://files.pythonhosted.org/packages/source/i/ink_extensions/ink_extensions-${_inkext_ver}.tar.gz"
)
sha256sums=('c29ef0792dc8a2006a3a4abcb306e8d7fa5b93f8ce83c0c781eed226d7eeca24'
            '5b6778073da34c6fafb5bd5f2a5e23ace9887dd29d6a9edaa41ce661083c7ba1'
            '68ac72552b589e5b8bb569af1c22eb8030f7c1485e9bf86f539f2cc1f2e4ee88')

_get_srcdir() { ls -d "$srcdir"/AxiDraw_API_* 2>/dev/null | head -n1; }

prepare() {
  cd "$srcdir"
  unzip -o AxiDraw_API.zip
  tar -xf "plotink-${_pink_ver}.tar.gz"
  tar -xf "ink_extensions-${_inkext_ver}.tar.gz"
}

build() {
  export PYTHONNOUSERSITE=1
  unset PYTHONUSERBASE

  # Build vendored deps first (offline)
  cd "$srcdir/plotink-${_pink_ver}"
  python -m build --wheel --no-isolation

  cd "$srcdir/ink_extensions-${_inkext_ver}"
  python -m build --wheel --no-isolation

  # Build EMSL package(s)
  local s=$(_get_srcdir)
  cd "$s"
  python -m build --wheel --no-isolation
  ls dist/*.whl >/dev/null 2>&1 || { echo "ERROR: no wheel produced"; return 1; }
}

package() {
  export PYTHONNOUSERSITE=1
  unset PYTHONUSERBASE

  # 1) vendored deps
  python -m pip install --root="$pkgdir" --prefix=/usr --no-deps --no-warn-script-location "$srcdir/plotink-${_pink_ver}"/dist/*.whl
  python -m pip install --root="$pkgdir" --prefix=/usr --no-deps --no-warn-script-location "$srcdir/ink_extensions-${_inkext_ver}"/dist/*.whl

  # 2) bundled third-party wheels (axidrawinternal, etc.)
  cd "$(_get_srcdir)"
  
  if ls prebuilt_dependencies/*.whl >/dev/null 2>&1; then
    python -m pip install --root="$pkgdir" --prefix=/usr --no-deps --no-warn-script-location prebuilt_dependencies/*.whl
  fi

  # 3) axicli + pyaxidraw
  python -m pip install --root="$pkgdir" --prefix=/usr --no-deps --no-warn-script-location dist/*.whl

  # license (best-effort)
  if [ -f "pyaxidraw/LICENSE.txt" ]; then
    install -Dm644 pyaxidraw/LICENSE.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  elif [ -f "LICENSE" ]; then
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  fi
}
