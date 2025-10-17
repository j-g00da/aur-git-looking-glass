# Maintainer: Dani Rodríguez <dani@danirod.es>
# Contributor: Carlos Aznarán <caznaranl@uni.pe>
# Contributor: Luis Martinez <luis dot martinez at disroot dot org>
# Contributor: Bjoern Franke <bjo+aur@schafweide.org>
# Contributor: Daniel Moch <daniel AT danielmoch DOT com>
# Contributor: gue5t <gue5t@aur.archlinux.org>
_base=Mastodon.py
pkgname=python-mastodon
pkgver=2.1.4
pkgrel=1
pkgdesc="Python wrapper for the Mastodon API"
arch=(any)
url="https://github.com/halcy/${_base}"
license=(MIT)
depends=(python-requests python-dateutil python-magic python-decorator python-halcy-blurhash)
makedepends=(python-build python-installer python-setuptools python-wheel)
optdepends=('python-cryptography: webpush support'
  'python-grapheme: support for the get_status_length function, if required'
  'python-http-ece: webpush support')
checkdepends=(python-pytest-runner python-pytest-cov python-pytest-vcr python-pytest-mock python-requests-mock python-pytz python-cryptography python-http-ece python-grapheme)
source=(${_base}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz)
sha512sums=('db644f23dfc4c1da86647592e5dd2090f19e657d2339b132c85d7d51c149e281d310f3b6c665ac4da169825e2cadbcc7ba005cb09c5bf5689f21fa62076c3e31')

build() {
  cd ${_base}-${pkgver}
  python -m build --wheel --no-isolation
}

check() {
  cd ${_base}-${pkgver}
  python -m venv --system-site-packages test-env
  test-env/bin/python -m pytest
}

package() {
  cd ${_base}-${pkgver}
  PYTHONPYCACHEPREFIX="${PWD}/.cache/cpython/" python -m installer --destdir="${pkgdir}" dist/*.whl
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
