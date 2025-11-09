# Maintainer: Daniel Bowring <aur@daniel.bowring.email>
# Maintainer: Daniele Paolella <danpaolella@gmail.com>
pkgname=gitbutler-bin
pkgver=0.17.6
pkgrel=1
_pkgvernum=2578
pkgdesc="Version control client, backed by Git, powered by Tauri/Rust/Svelte"
arch=('x86_64')
url="https://gitbutler.com/"
depends=('libayatana-appindicator' 'webkit2gtk-4.1' 'gtk3')
license=('LicenseRef-FSL-1.1-MIT')
source=("https://releases.gitbutler.com/releases/release/${pkgver}-${_pkgvernum}/linux/$CARCH/GitButler_${pkgver}_amd64.deb"
        "LICENSE.md")
sha256sums=('a5250676798b8ba2ba1033c21353e19951c4652a5b8ff53b3a9b0420b271e063'
            '2a3154bf44e0b219014291b96249082f3305844a1d73796741468c8128c2829e')

package() {
	bsdtar -xf "$srcdir/data.tar.gz" -C "$pkgdir"
	install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
