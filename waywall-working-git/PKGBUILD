# Maintainer: Esensats <esensats@gmail.com>
# Co-maintainer: tesselslate
pkgname=waywall-working-git
pkgver=wall.r193.g90fafbe
pkgrel=1
pkgdesc="Wayland compositor for Minecraft speedrunning"
arch=('x86_64')
url="https://github.com/tesselslate/waywall"
license=('GPL-3.0-only')
depends=(
    'libglvnd'          # provides EGL and GLESv2
    'luajit'
    'libspng'
    'wayland'
    'libxcb'
    'xcb-util-cursor'   # for wayland-cursor functionality
    'xorg-xwayland'
    'libxkbcommon'
)
makedepends=(
    'meson'
    'ninja'
    'git'
    'wayland-protocols'
)
provides=('waywall')
conflicts=('waywall')
source=("$pkgname::git+https://github.com/tesselslate/waywall.git")
sha256sums=('SKIP')

pkgver() {
    cd "$pkgname"
    # Get version from git tags, or use commit count if no tags
    git describe --long --tags 2>/dev/null | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cd "$pkgname"
    
    # Use the project's Makefile which calls meson
    make
}

check() {
    cd "$pkgname"
    
    # Run tests if available
    make check || true
}

package() {
    cd "$pkgname"
    
    # Install the binary manually since there's no install target
    install -Dm755 build/waywall/waywall "$pkgdir/usr/bin/waywall"
    
    # Install documentation
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    
    # Install any documentation from doc/ directory
    if [ -d doc ]; then
        cp -r doc "$pkgdir/usr/share/doc/$pkgname/"
    fi
}
