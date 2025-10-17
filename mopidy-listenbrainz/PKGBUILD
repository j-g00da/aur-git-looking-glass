# Maintainer: Kannan Thambiah <pygospa at gmail dot com>

pkgname=mopidy-listenbrainz
pkgver=0.3.0
pkgrel=1
pkgdesc="Mopidy extension for scrobbling played tracks to listenbrainz"
arch=("any")
url="https://github.com/suaviloquence/mopidy-listenbrainz"
license=("Apache-2.0")
depends=(
	"mopidy"
	"python"
	"python-musicbrainzngs"
	"python-pykka"
	"python-requests"
	"python-setuptools"
)
makedepends=(
	"python-build"
	"python-installer"
	"python-wheel"
)

source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('df6695faff53ca359ccdb560284904f8d85c6761c4593cc320061f5ef880460c')

build() {
	cd "$pkgname-$pkgver"
	python -m build --wheel --no-isolation
}

package() {
	cd "$pkgname-$pkgver"
	python -m installer --destdir="$pkgdir" dist/*.whl
}

