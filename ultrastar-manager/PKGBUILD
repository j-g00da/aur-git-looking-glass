# Maintainer: Jonas Bögle <aur@iwr.sh>
# Contributor: Alexander Blinne

pkgname=ultrastar-manager
pkgver=r1244.c2ba185
pkgrel=1
pkgdesc="Qt program used to manage USDX songs"
url=https://github.com/UltraStar-Deluxe/UltraStar-Manager
license=('GPL2')
arch=('x86_64')

depends=('qt6-base' 'qt6-multimedia' 'libmediainfo' 'taglib' 'cld2-git' 'pulseaudio-alsa' 'libebur128')
makedepends=('qt6-tools' 'git')

source=('git+https://github.com/UltraStar-Deluxe/UltraStar-Manager.git')

md5sums=('SKIP')

pkgver() {
  cd "$srcdir/UltraStar-Manager"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build()
{
	cd "$srcdir/UltraStar-Manager"
	qmake6
	make
}

package()
{
	cd "$srcdir/UltraStar-Manager"
	install -Dm644 "setup/unix/UltraStar-Manager.png" "${pkgdir}/usr/share/pixmaps/UltraStar-Manager.png"
	install -Dm644 "setup/unix/UltraStar-Manager.desktop" "${pkgdir}/usr/share/applications/UltraStar-Manager.desktop"

	cd "$srcdir/UltraStar-Manager/bin/"
	mkdir -m755 ${pkgdir}/opt
	cp -r release ${pkgdir}/opt/UltraStar-Manager
	chmod -R u=rwX,go=rX ${pkgdir}/opt/UltraStar-Manager

	mkdir -pm755 ${pkgdir}/usr/bin
	ln -s /opt/UltraStar-Manager/UltraStar-Manager ${pkgdir}/usr/bin/UltraStar-Manager
}
