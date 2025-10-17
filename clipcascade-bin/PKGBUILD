# Maintainer: Seunghun Kim <seunghunkim at proton dot me>
pkgname=clipcascade-bin
pkgver=3.1.0
pkgrel=1
pkgdesc="ClipCascade: Sync clipboard across multiple devices"
arch=('x86_64')
url="https://github.com/Sathvik-Rao/ClipCascade"
license=('GPL-3.0')
depends=(
    'tk'
    'python'
    'python-pillow'
    'python-plyer'
    'python-pycryptodome'
    'python-pystray'
    'python-requests'
    'python-websocket-client'
    'python-xxhash'
    'python-pyfiglet'
    'python-beautifulsoup4'
    'python-aiortc'
    'python-ifaddr'
    'xclip'
)
makedepends=('unzip')
source=(
    "$url/releases/download/$pkgver/ClipCascade_Linux.zip"
    "clipcascade.png::https://raw.githubusercontent.com/Sathvik-Rao/ClipCascade/refs/tags/3.1.0/logo/logo.png"
    "clipcascade.desktop"
    "fix-write-path.patch"
)
sha256sums=(
    '66c02e84c47cdc9eb2686ab551f52bbfb38fbce091e2a54002807612afd2c65f'
    '54974fabd99d918ea142163db566a98d3ca1a43b5a0f3d0c7ed7224ecccbd3b9'
    '6b90177c1c1ed1e575cb1f553cd2cde4b2b92d32743e32ec046aaf2ed3674594'
    'c831a463b7ddb2e22d53e5f80996e3305183ff88d671a32f73000783f71df13f'
)

prepare() {
    unzip -o "${srcdir}/ClipCascade_Linux.zip" -d "${srcdir}/ClipCascade"
    cd "${srcdir}/ClipCascade"
    patch -p1 < "${srcdir}/fix-write-path.patch"
}

package() {
    install -d "${pkgdir}/usr/share/clipcascade"
    cp -r "${srcdir}/ClipCascade/"* "${pkgdir}/usr/share/clipcascade/"

    install -d "${pkgdir}/usr/bin"
    install -Dm755 /dev/stdin "${pkgdir}/usr/bin/clipcascade" << EOF
#!/bin/sh
# Create ~/.clipcascade if it doesn't exist
[ -d "\${HOME}/.clipcascade" ] || mkdir -p "\${HOME}/.clipcascade"
exec python /usr/share/clipcascade/main.py "\$@"
EOF

    install -Dm644 "${srcdir}/ClipCascade/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm644 "${srcdir}/clipcascade.desktop" "${pkgdir}/usr/share/applications/clipcascade.desktop"
    install -Dm644 "${srcdir}/clipcascade.png" "${pkgdir}/usr/share/pixmaps/clipcascade.png"
}
