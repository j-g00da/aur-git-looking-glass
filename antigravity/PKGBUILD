pkgname=antigravity
pkgver=1.11.2
pkgrel=1
pkgdesc="Google Antigravity is an agentic development platform, evolving the IDE into the agent-first era."
arch=('x86_64')
url="https://antigravity.google/"
license=('custom')
depends=('gtk3' 'nss' 'alsa-lib' 'libxss' 'libxtst' 'xdg-utils' 'libdrm' 'mesa' 'glibc' 'nspr' 'at-spi2-core')
source=(
  "Antigravity.tar.gz::https://edgedl.me.gvt1.com/edgedl/release2/j0qc3/antigravity/stable/${pkgver}-6251250307170304/linux-x64/Antigravity.tar.gz"
  "antigravity.png"
)
sha256sums=('d1b1115ae76c275c376ea660e1e4d2dc20eb3e72d6a206b096505b944a5f64b7'
            'ba0688b8ead9daf9609110ed782b9c47f3c57be74e9c276ec2b49e411dd4020b')

package() {
  cd "$srcdir/Antigravity"

  install -d "$pkgdir/opt/antigravity"
  cp -a ./* "$pkgdir/opt/antigravity/"

  # Chromium sandbox permissions
  if [[ -f "$pkgdir/opt/antigravity/chrome-sandbox" ]]; then
    chmod 4755 "$pkgdir/opt/antigravity/chrome-sandbox"
  fi

  # Symlink binary (adjust if wrong)
  install -d "$pkgdir/usr/bin"
  ln -s /opt/antigravity/Antigravity "$pkgdir/usr/bin/antigravity"

  # Icon
  install -Dm644 "$srcdir/antigravity.png" "$pkgdir/usr/share/pixmaps/antigravity.png"

  # Desktop entry
  install -d "$pkgdir/usr/share/applications"
  cat > "$pkgdir/usr/share/applications/antigravity.desktop" <<EOF
[Desktop Entry]
Type=Application
Name=Antigravity
Exec=antigravity
Icon=antigravity
Categories=Development;IDE;
StartupWMClass=Antigravity
EOF
}
