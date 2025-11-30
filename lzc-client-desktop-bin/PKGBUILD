# Maintainer: Your Name <your.email@example.com>
pkgname=lzc-client-desktop-bin
pkgver=1.6.0
pkgrel=1
pkgdesc='Lazy Cat microservice desktop client'
arch=('x86_64')
url='https://lazycat.cloud/'
license=('custom')
depends=(
  'zenity'
  'libcap'
  'glib2'
  'nspr'
  'nss'
  'dbus'
  'at-spi2-core'
  'libcups'
  'cairo'
  'gtk3'
  'pango'
  'libx11'
  'libxcomposite'
  'libxdamage'
  'libxext'
  'libxfixes'
  'libxrandr'
  'mesa'
  'expat'
  'libxcb'
  'libxkbcommon'
  'systemd-libs'
  'alsa-lib'
)
makedepends=('zstd')
install="${pkgname}.install"
source=("lzc-client-desktop_${pkgver}.tar.zst::https://dl.lazycat.cloud/client/desktop/stable/lzc-client-desktop_v${pkgver}.tar.zst")
sha256sums=('23ae44472ba72bc7a722b04995c781b3e1073f0324ab02e47cc4e4304904a2ac')

# Disable compression for faster testing during development
# Remove this line before publishing to AUR
PKGEXT='.pkg.tar'

package() {
  cd "$srcdir"

  # Files extract directly to srcdir, not in a subdirectory
  _appdir="."

  # 1. Install application files to /usr/lib/lzc-client-desktop
  msg "Installing application files..."
  install -dm755 "$pkgdir/usr/lib/lzc-client-desktop"

  # Copy all application files (adjust based on actual structure)
  cp -a "$_appdir"/* "$pkgdir/usr/lib/lzc-client-desktop/" 2>/dev/null || true

  # Ensure binary is executable
  if [ -f "$pkgdir/usr/lib/lzc-client-desktop/lzc-client-desktop" ]; then
    chmod +x "$pkgdir/usr/lib/lzc-client-desktop/lzc-client-desktop"
  fi

  # Set chrome-sandbox permissions (required for Electron apps)
  if [ -f "$pkgdir/usr/lib/lzc-client-desktop/chrome-sandbox" ]; then
    chmod 4755 "$pkgdir/usr/lib/lzc-client-desktop/chrome-sandbox"
  fi

  # 2. Create wrapper script in /usr/bin
  msg "Creating wrapper script..."
  install -Dm755 /dev/stdin "$pkgdir/usr/bin/lzc-client-desktop" <<'EOF'
#!/bin/bash
# Wrapper script for lzc-client-desktop
exec /usr/lib/lzc-client-desktop/lzc-client-desktop "$@"
EOF

  # 3. Install desktop file with corrected paths
  msg "Installing desktop file..."
  if [ -f "$_appdir/lzc-client.desktop" ]; then
    install -Dm644 "$_appdir/lzc-client.desktop" \
      "$pkgdir/usr/share/applications/lzc-client-desktop.desktop"

    # Patch Exec path to use /usr/bin wrapper
    sed -i \
      -e 's|^Exec=.*|Exec=/usr/bin/lzc-client-desktop|g' \
      -e 's|HOMEDIR|/usr/lib/lzc-client-desktop|g' \
      "$pkgdir/usr/share/applications/lzc-client-desktop.desktop"
  fi

  # 4. Install icon if present
  msg "Installing icon..."
  # Try common icon locations and names
  for icon_path in \
    "$_appdir/icon.png" \
    "$_appdir/lzc-client-desktop.png" \
    "$_appdir/resources/icon.png" \
    "$_appdir/share/icons/lzc-client-desktop.png"
  do
    if [ -f "$icon_path" ]; then
      install -Dm644 "$icon_path" \
        "$pkgdir/usr/share/pixmaps/lzc-client-desktop.png"
      break
    fi
  done

  # 5. Install polkit policy if present
  msg "Installing polkit policy..."
  if [ -f "$_appdir/cloud.lazycat.client.policy" ]; then
    install -Dm644 "$_appdir/cloud.lazycat.client.policy" \
      "$pkgdir/usr/share/polkit-1/actions/cloud.lazycat.client.policy"

    # Patch script paths in polkit policy to use system paths
    sed -i \
      -e 's|HOMEDIR|/usr/lib/lzc-client-desktop|g' \
      -e "s|/home/[^/]*/[^<]*|/usr/lib/lzc-client-desktop/lzc-client-desktop|g" \
      "$pkgdir/usr/share/polkit-1/actions/cloud.lazycat.client.policy"
  fi

  # 6. Handle capabilities
  # Note: Capabilities will be set during post_install via the .install script
  # This is the recommended approach for AUR packages

  # 7. Install license if present
  msg "Installing license..."
  for license_file in \
    "$_appdir/LICENSE" \
    "$_appdir/LICENSE.txt" \
    "$_appdir/COPYING"
  do
    if [ -f "$license_file" ]; then
      install -Dm644 "$license_file" \
        "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
      break
    fi
  done

  # Create a placeholder license file if none found
  if [ ! -f "$pkgdir/usr/share/licenses/$pkgname/LICENSE" ]; then
    install -Dm644 /dev/stdin "$pkgdir/usr/share/licenses/$pkgname/LICENSE" <<EOF
Proprietary software from Lazy Cat (lazycat.cloud)
License terms available at: https://lazycat.cloud/
EOF
  fi

  # 8. Remove any bundled setcap scripts to prevent self-modification
  rm -f "$pkgdir/usr/lib/lzc-client-desktop/set-capabilities.sh"

  # 9. Clean up unnecessary files from /usr/lib
  rm -f "$pkgdir/usr/lib/lzc-client-desktop"/*.desktop
  rm -f "$pkgdir/usr/lib/lzc-client-desktop"/*.policy
  rm -f "$pkgdir/usr/lib/lzc-client-desktop"/*.png
}
