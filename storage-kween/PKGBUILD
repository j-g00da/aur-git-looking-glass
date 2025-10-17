pkgname=storage-kween
pkgver=0.1.1
pkgrel=1
pkgdesc="An elegant GUI storage cleaner for Arch Linux users"
arch=('any')
url="https://github.com/drainch/storage-kween"
license=('MIT')
depends=('python' 'python-dearpygui' 'fdupes' 'util-linux' 'pacman-contrib')
optdepends=(
  'zenity: optional GUI dialogs'
  'file: media type detection'
  'imagemagick: image analysis'
  'python-pillow: image processing'
)
source=("https://github.com/drainch/storage-kween/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('SKIP')

package() {
  cd "$srcdir/storage-kween-$pkgver"

  install -Dm755 storage-kween.py "$pkgdir/usr/bin/storage-kween"
  install -Dm644 storage-kween.desktop "$pkgdir/usr/share/applications/storage-kween.desktop"
}

