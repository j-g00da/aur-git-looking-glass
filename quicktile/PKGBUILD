# Maintainer: Luke Arms <luke@arms.to>
# Contributor: dustball

pkgname=quicktile
pkgver=0.4.1
pkgrel=1
url="https://github.com/ssokolow/quicktile"
pkgdesc="Adds window-tiling hotkeys to any X11 desktop"
arch=('any')
license=('GPL-2.0-or-later')
depends=('python' 'gtk3' 'libwnck3' 'python-gobject' 'python-xlib')
optdepends=('python-dbus: required if you want to interact with QuickTile over D-Bus')
makedepends=('python-setuptools')
conflicts=('quicktile-git')
source=(
  "https://github.com/ssokolow/quicktile/archive/v${pkgver}.tar.gz"
)
sha512sums=('f5ceea0a909f7ac3884d6d4300e8c62ff3d4f53c475b34fb551530b78ce4c223ebac62d765e72c6c56e534ab50823d5b5bb1a8089c5944f6e29f2fc90e617c4f')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  python setup.py build
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  python setup.py install --root="$pkgdir" --optimize=1 --skip-build
}
