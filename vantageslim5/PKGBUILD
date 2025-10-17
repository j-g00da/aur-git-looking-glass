# Maintainer: Luís Pereira <lumafepe@gmail.com>
pkgname=vantageslim5
pkgver=1.0.1
pkgrel=1
pkgdesc="Tray application for managing Lenovo vantage settings for the Legion Slim5 14APH8"
arch=('any')
url="https://github.com/lumafepe/VantageSlim5"
license=('MIT')
depends=('python' 'python-pyqt5' 'polkit')
makedepends=('python-setuptools')
source=("lenovo_tray.py"
        "requirements.txt")
sha256sums=('6e3a6edef0c7d30afd7a712e07ef580de861252b048b736cbb9cc00e76e78a28'
            '62b74a677578752612cbb62f36d7e0fbd4c3633008ce1b50c991abe3ce77cce8')

prepare() {
	:
}

build() {
	:
}

check() {
	:
}

package() {
	# Install the Python script
	install -Dm755 "$srcdir/lenovo_tray.py" "$pkgdir/usr/bin/vantageslim5"
	
	# Install requirements as documentation
	install -Dm644 "$srcdir/requirements.txt" "$pkgdir/usr/share/doc/$pkgname/requirements.txt"
}
