# Maintainer: Daniel Bowring <aur@daniel.bowring.email>
# Maintainer: Daniele Paolella <danpaolella@gmail.com>
pkgname=gitbutler-bin
pkgver=0.18.0
pkgrel=1
_pkgvernum=2626
pkgdesc="Version control client, backed by Git, powered by Tauri/Rust/Svelte"
arch=('x86_64')
url="https://gitbutler.com/"
depends=('libayatana-appindicator' 'webkit2gtk-4.1' 'gtk3')
license=('LicenseRef-FSL-1.1-MIT')
source=("https://releases.gitbutler.com/releases/release/${pkgver}-${_pkgvernum}/linux/$CARCH/GitButler_${pkgver}_amd64.deb"
        "LICENSE.md")
sha256sums=('74bbd378a5eda175d1c1cd2f111d905857af39d43ef5ffcf0c600814011087b6'
            '2a3154bf44e0b219014291b96249082f3305844a1d73796741468c8128c2829e')

package() {
	bsdtar -xf "$srcdir/data.tar.gz" -C "$pkgdir"
	install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
