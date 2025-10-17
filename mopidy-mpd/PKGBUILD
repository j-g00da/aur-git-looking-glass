# Maintainer: Kannan Thambiah <pygospa at gmail dot com>
# Contributor: Johannes Wienke <languitar@semipol.de>
# Contributor: bittin

pkgname=mopidy-mpd
pkgver=3.3.0
pkgrel=3
pkgdesc="Mopidy extension for controlling playback from MPD clients"
arch=('any')
url="http://www.mopidy.com"
license=('Apache-2.0')
depends=(
	'mopidy>=3.0'
	'glib2'
	'python'
	'python-gobject'
	'python-pykka'
	'python-setuptools'
)
makedepends=('python3' 'python-setuptools')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/mopidy/mopidy-mpd/archive/v${pkgver}.tar.gz" "fix-playid.patch")
sha256sums=('69ac13e79d3f77452e49722fe3322e6e60cb39fe24556153a7b3a119a5b3a893'
            '7bf5c45e8eaed515712324ea7074b10b025151e74c50e9355647ca2071f88f07')

prepare() {
	cd "$srcdir/$pkgname-$pkgver"
	patch -Np1 -i "$srcdir/fix-playid.patch"
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    python3 setup.py install --root="$pkgdir/" --optimize=1
}
