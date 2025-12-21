# Maintainer: AlphaLynx <alphalynx at alphalynx dot dev>

pkgname=antigravity
pkgver=1.13.3
pkgrel=1
pkgdesc='An agentic development platform from Google, evolving the IDE into the agent-first era.'
arch=('aarch64' 'x86_64')
url='https://antigravity.google/'
license=('LicenseRef-Google-Antigravity')
depends=(
    'alsa-lib'
    'at-spi2-core'
    'bash'
    'cairo'
    'dbus'
    'expat'
    'gcc-libs'
    'glib2'
    'glibc'
    'gtk3'
    'libcups'
    'libx11'
    'libxcb'
    'libxcomposite'
    'libxdamage'
    'libxext'
    'libxfixes'
    'libxkbcommon'
    'libxkbfile'
    'libxrandr'
    'mesa'
    'nspr'
    'nss'
    'pango'
    'systemd-libs'
)
options=(!strip !debug)
source_aarch64=("Antigravity-$pkgver-aarch64.deb::https://us-central1-apt.pkg.dev/projects/$pkgname-auto-updater-dev/pool/$pkgname-debian/${pkgname}_$pkgver-1766182168_arm64_940bc88042cadeaee51d9b1eedf6a506.deb")
source_x86_64=("Antigravity-$pkgver-x86_64.deb::https://us-central1-apt.pkg.dev/projects/$pkgname-auto-updater-dev/pool/$pkgname-debian/${pkgname}_$pkgver-1766182170_amd64_365061c50063f9bd47a9ff88432261b8.deb")
sha256sums_aarch64=('9d4d5a0f4dc39514a8841e726bf032e19f8baf42310ed11531cd95d43922c14e')
sha256sums_x86_64=('d9920f9e0788245b1dab0f73a607b4eea00605bfb70e16795da1c1ac89eabd4b')
b2sums_aarch64=('b77141c125a785d937e1ea74aad9baa842008e849330130335592ff47c4f701bd6faa20a7bce5611882cc4d6578bcae16d0122ab86403153272f84fa21bb8e30')
b2sums_x86_64=('ac9a11ee619b795d854383351401265fd1b8e08e74f0487c5b55985974cef90773c6c94c4968eb7ea10b2710e8579af0a8288ef448050d10878da4b08f786734')

package() {
    tar -xf data.tar.xz --no-same-owner -C "$pkgdir/"

    install -dm755 "$pkgdir/opt"
    mv "$pkgdir/usr/share/$pkgname" "$pkgdir/opt/Antigravity"

    install -dm755 "$pkgdir/usr/bin"
    ln -s /opt/Antigravity/bin/$pkgname "$pkgdir/usr/bin/$pkgname"

    sed -i 's|/usr/share/antigravity|/opt/Antigravity|g' "$pkgdir/usr/share/applications/"*.desktop

    install -dm755 "$pkgdir/usr/share/metainfo"
    mv "$pkgdir/usr/share/appdata/$pkgname.appdata.xml" \
        "$pkgdir/usr/share/metainfo/$pkgname.appdata.xml"
    rmdir "$pkgdir/usr/share/appdata"

    install -dm755 "$pkgdir/usr/share/licenses/$pkgname"
    ln -s /opt/Antigravity/resources/app/LICENSE.txt \
        "$pkgdir/usr/share/licenses/$pkgname/LICENSE.txt"
    ln -s /opt/Antigravity/LICENSES.chromium.html \
        "$pkgdir/usr/share/licenses/$pkgname/LICENSES.chromium.html"
}
