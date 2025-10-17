# Maintainer: Your Name <your.email@example.com>
pkgname=goclock
pkgver=1.0.0
pkgrel=1
pkgdesc="A simple and elegant desktop clock application"
arch=('x86_64' 'i686' 'arm' 'armv6h' 'armv7h' 'aarch64')
url="https://github.com/AnnNaserNabil/goclock"
license=('MIT')
depends=('gtk3' 'glib2' 'libx11' 'libxext' 'libxrender' 'libxrandr' 'libxinerama' 'libxcursor' 'libxi' 'libxcomposite' 'libxdamage' 'libxfixes' 'libxau' 'libxdmcp' 'libxcb')
makedepends=('go' 'git' 'pkgconf' 'gcc' 'glu')
provides=('goclock')
conflicts=('goclock')

build() {
    cd "$srcdir/.."
    
    # Initialize Go module if not already done
    if [ ! -f go.mod ]; then
        go mod init github.com/AnnNaserNabil/goclock
    fi
    
    # Get dependencies
    go mod tidy
    
    # Build
    go build -o goclock
}

package() {
    cd "$srcdir/.."
    
    # Install binary
    install -Dm755 goclock "$pkgdir/usr/bin/goclock"
    
    # Install license
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    
    # Install .desktop file
    mkdir -p "$pkgdir/usr/share/applications"
    cat > "$pkgdir/usr/share/applications/goclock.desktop" << EOF
[Desktop Entry]
Type=Application
Name=Go Clock
Comment=A simple and elegant desktop clock application
Exec=/usr/bin/goclock
Icon=clock
Categories=Utility;
Terminal=false
EOF
}
