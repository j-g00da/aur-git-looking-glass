# Maintainer: Liam Busby <busby.liam@protonmail.com>
pkgname=elysium
pkgver=1.3.0
pkgrel=4
pkgdesc="A custom file explorer"
arch=('x86_64')
url="https://www.elysiumfiles.co.uk"
license=('custom')
depends=('python')
makedepends=('pyinstaller')
source=("$pkgname::git+https://github.com/buzby08/Elysium.git")
sha256sums=('SKIP')


build() {
	cd "$srcdir/$pkgname"
	pyinstaller --clean --noconfirm Elysium-linux.spec
}

package() {
	cd "$srcdir/$pkgname/dist/Elysium"
	install -Dm755 "Elysium" "$pkgdir/usr/bin/Elysium"
	cp -r "_internal" "$pkgdir/usr/bin/_internal"
	install -Dm644 "$srcdir/$pkgname/LICENSE.md" "$pkgdir/usr/share.licences/$pkgname/LICENSE"
	install -Dm644 "$srcdir/$pkgname/Elysium.desktop" \
		"$pkgdir/usr/share/applications/Elysium.desktop"
	install -Dm644 "$srcdir/$pkgname/Images/ElysiumLogo.png" \
		"$pkgdir/usr/share/pixmaps/Elysium.png"
}
