# Maintainer: Webarch <contact@webarch.ro>
# Generated on: 2025-12-06 21:27:31 UTC

pkgname=windsurf-next
pkgver=1.12.157_next.10ebfa84f4
pkgrel=1
pkgdesc="Windsurf-next - Next version of the Windsurf editor"
arch=('x86_64')
url="https://windsurf.com"
license=('Custom')
depends=(
    'vulkan-driver'
    'ffmpeg'
    'glibc'
    'libglvnd'
    'gtk3'
    'alsa-lib'
)
makedepends=('curl' 'jq')
optdepends=(
    'bash-completion: for bash shell completions'
    'zsh: for zsh shell completions'
)
provides=("$pkgname")
conflicts=("$pkgname")
options=('!strip')

# Use a variable for the downloaded filename for clarity
_pkgfilename="windsurf-next_1.12.157_next.10ebfa84f4_linux-x64"

source=(
    # Download the main binary, renaming it using :: syntax
    "$_pkgfilename::https://windsurf-stable.codeiumdata.com/linux-x64/next/10ebfa84f4e8b018ef2459063f0293b8e9ac01da/Windsurf-linux-x64-1.12.157+next.10ebfa84f4.tar.gz"
    # Include the local .desktop file
    'windsurf-next.desktop'
    # Include the URL handler .desktop file
    'windsurf-next-url-handler.desktop'
)
sha256sums=('1ce3afc1589a9498dfecd58bb4e632625513245fb43d814a2836e28da10a29be'
            '0561a3546b31291d43138b1f51e9696d889b37d0e88966c9bd32307d4536f91a'
            '7bcdc177ae93096a04076ddf519b836dddf3a11a49e19bfca80f6bf5e60f91b2'
           )

package() {
    cd "$srcdir"

    # Extract the tarball to a temporary directory
    mkdir -p windsurf-extract
    tar -xzf "$_pkgfilename" -C windsurf-extract --strip-components=1
    
    # Create the target directory in /opt
    install -dm755 "$pkgdir/opt/$pkgname"
    
    # Copy all files to the target directory
    cp -r windsurf-extract/* "$pkgdir/opt/$pkgname/"
    
    # Create symlink for the executable
    install -dm755 "$pkgdir/usr/bin"
    ln -sf "/opt/$pkgname/$pkgname" "$pkgdir/usr/bin/$pkgname"

    # Install the desktop entry file
    install -Dm644 "$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
    
    # Install the URL handler desktop entry file
    install -Dm644 "$pkgname-url-handler.desktop" "$pkgdir/usr/share/applications/$pkgname-url-handler.desktop"

    # Install bash completion
    install -Dm644 "windsurf-extract/resources/completions/bash/$pkgname" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
    
    # Install zsh completion
    install -Dm644 "windsurf-extract/resources/completions/zsh/_$pkgname" "$pkgdir/usr/share/zsh/site-functions/_$pkgname"
    
    # Install icon
    install -Dm644 "windsurf-extract/resources/app/resources/linux/code-next.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
    
    # Fix permissions
    chmod 755 "$pkgdir/opt/$pkgname/$pkgname"
    chmod 4755 "$pkgdir/opt/$pkgname/chrome-sandbox"
}
