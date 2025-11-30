# Partially based on fluent-icon-theme (I just wanted the icon theme, but
# having the cursor theme too looks convenient.)

# Maintainer: Dani Rodriguez <dani@danirod.es>
pkgname=('mactahoe-icon-theme-git' 'mactahoe-cursor-theme-git')
pkgbase=mactahoe-icon-theme-git
pkgver=2025.10.16.r1.9669dfee
pkgrel=1
pkgdesc="MacOS Tahoe icon theme for Linux"
arch=('any')
url="https://github.com/vinceliuice/MacTahoe-icon-theme"
license=('GPL-3.0-or-later')
depends=(
  'gtk-update-icon-cache'
  'hicolor-icon-theme'
)
makedepends=('git')
options=('!strip')
source=('git+https://github.com/vinceliuice/MacTahoe-icon-theme.git')
sha256sums=('SKIP')

pkgver() {
	cd MacTahoe-icon-theme
	printf "%s" "$(git describe --long --tags | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}

prepare() {
  cd MacTahoe-icon-theme

  # Do not run gtk-update-icon-cache
  sed -i '/gtk-update-icon-cache/d' install.sh

  # Do not install cursors unless the cursor package is installed
  sed -i 's/install_theme && install_cursor_theme/install_theme/' install.sh
}

package_mactahoe-icon-theme-git() {
  provides=("${pkgname%-git}")
  conflicts=("${pkgname%-git}")

  cd MacTahoe-icon-theme
  install -d "$pkgdir/usr/share/icons"
  ./install.sh -d "$pkgdir/usr/share/icons" -t all
}

package_mactahoe-cursor-theme-git() {
	pkgdesc="MacOS Tahoe like cursor theme for Linux desktops (based on Qogir cursors)"
	provides=("${pkgname%-git}")
	conflicts=("${pkgname%-git}")

	cd MacTahoe-icon-theme/cursors
	install -d "$pkgdir/usr/share/icons"
	cp -r dist "$pkgdir/usr/share/icons/MacTahoe-cursors"
	cp -r dist-dark "$pkgdir/usr/share/icons/MacTahoe-dark-cursors"
}
