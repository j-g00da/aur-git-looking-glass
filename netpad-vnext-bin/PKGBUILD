# Maintainer: Ersin <ersin@example.com>
pkgname=netpad-vnext-bin
pkgver=0.10.0
pkgrel=1
pkgdesc="A cross-platform C# editor and playground (vNext - Rust-based shell)"
arch=('x86_64')
url="https://github.com/tareqimbasher/NetPad"
license=('MIT')
depends=('dotnet-runtime>=9.0')
provides=('netpad-vnext')
conflicts=('netpad-vnext')
source=("https://github.com/tareqimbasher/NetPad/releases/download/v${pkgver}/netpad_vnext-${pkgver}-linux-amd64.deb")
sha256sums=('SKIP')

package() {
    # Extract .deb package
    cd "${srcdir}"
    ar x "netpad_vnext-${pkgver}-linux-amd64.deb"
    tar -xzf data.tar.gz -C "${pkgdir}"

    # Fix permissions
    chmod +x "${pkgdir}/usr/bin/netpad-vnext"

    # Create desktop entry
    install -Dm644 /dev/stdin "${pkgdir}/usr/share/applications/netpad-vnext.desktop" <<EOF
[Desktop Entry]
Name=NetPad vNext
Comment=Cross-platform C# editor and playground (Rust-based)
Exec=/usr/bin/netpad-vnext
Icon=netpad-vnext
Terminal=false
Type=Application
Categories=Development;IDE;
EOF
}
