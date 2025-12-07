# Maintainer: AlphaLynx <alphalynx at alphalynx dot dev>

pkgname=antigravity
pkgver=1.11.14
pkgrel=1
pkgdesc='An agentic development platform from Google, evolving the IDE into the agent-first era.'
arch=('x86_64')
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
source=("$pkgname-$pkgver.tar.gz::https://edgedl.me.gvt1.com/edgedl/release2/j0qc3/antigravity/stable/$pkgver-5763785964257280/linux-x64/Antigravity.tar.gz"
        "antigravity.desktop"
        "antigravity-url-handler.desktop")
b2sums=('654df78b7c62e06028de0b346a2825b93653a2e876145dd45940e002a7e050c01db04fa0f16857b07fde7282e93e421a17cf095f57e3ce95624f62b37e077a32'
        '59dc67f1cb2f06e77aa1e3496ebcdfc7b8182f94b6cec53f727c8644486b5259ac6683cc7db61dfa4ce5d468e96737290256529e44cc171adcd8dc4e106b3dbb'
        '99042366cd8f3a4da093234903d755106ed895afafbe203c253927322126c70cfe75f28ca0bfb345688478f786f22f33e1e58c5e14479030f9babf32193c9071')

package() {
    install -dm755 "$pkgdir/opt/Antigravity"
    cp -a Antigravity/* "$pkgdir/opt/Antigravity/"

    install -dm755 "$pkgdir/usr/bin"
    ln -s /opt/Antigravity/bin/$pkgname "$pkgdir/usr/bin/$pkgname"

    install -Dm644 $pkgname.desktop \
        "$pkgdir/usr/share/applications/$pkgname.desktop"
    install -Dm644 $pkgname-url-handler.desktop \
        "$pkgdir/usr/share/applications/$pkgname-url-handler.desktop"

    install -dm755 "$pkgdir/usr/share/pixmaps"
    ln -s /opt/Antigravity/resources/app/resources/linux/code.png \
        "$pkgdir/usr/share/pixmaps/$pkgname.png"

    install -dm755 "$pkgdir/usr/share/licenses/$pkgname"
    ln -s /opt/Antigravity/resources/app/LICENSE.txt \
        "$pkgdir/usr/share/licenses/$pkgname/LICENSE.txt"
    ln -s /opt/Antigravity/LICENSES.chromium.html \
        "$pkgdir/usr/share/licenses/$pkgname/LICENSES.chromium.html"
}
