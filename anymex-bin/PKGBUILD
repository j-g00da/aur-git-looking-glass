# Based off of: https://daveparrish.net/posts/2019-11-16-Better-AppImage-PKGBUILD-template.html
# Maintainer: jullanggit <jullanggit@proton.me>

_pkgname=anymex
_PkgName=AnymeX # capitalised name
pkgname=$_pkgname-bin
pkgver=3.0.1_hotfix
pkgrel=1
arch=(x86_64) # not sure if arm is also supported on linux
pkgdesc='An Open Source app for Tracking Multi Service (AL, MAL, SIMKL)'
url="https://github.com/RyanYuuki/$_PkgName"
license=(MIT)
provides=($_pkgname=$pkgver)
depends=(
  'libepoxy'
  'gdk-pixbuf2'
  'pango'
  'webkit2gtk-4.1'
  'harfbuzz'
  'libsoup3'
  'glibc'
  'fontconfig'
  'cairo'
  'hicolor-icon-theme'
  'glib2'
  'gcc-libs'
  'mpv'
  'zlib-ng-compat'
  'gtk3'
  'at-spi2-core'
)
conflicts=(anymex)
_appimage="$_PkgName-$pkgver.AppImage"
source=("$_appimage::$url/releases/download/v${pkgver//_/-}/$_PkgName-Linux.AppImage"
  "LICENSE-$pkgver.md::https://raw.githubusercontent.com/RyanYuuki/AnymeX/refs/tags/v${pkgver//_/-}/LICENSE.md")
noextract=($_appimage)
sha256sums=('9560dadcac9027f71b44a5dd084a0d5f5ecfc67091f3a47c6137ac12f8611843'
            '20e150fbf9ff46e419434750d9034d40e4fe6a1a5dac37aaf8541dca69c2e02f')

prepare() {
  chmod +x $_appimage
  ./$_appimage --appimage-extract >/dev/null
}

build() {
  # Fix permissions; .AppImage permissions are 700 for all directories
  chmod -R a-x+rX squashfs-root/usr

  chmod +x squashfs-root/usr/bin/anymex
}

package() {
  # application
  install -dm755 "$pkgdir/usr/"
  mv "$srcdir"/squashfs-root/usr/* "$pkgdir/usr/" # cp -a for some reason messes up directory permissions

  # license
  install -Dm644 "$srcdir/LICENSE-$pkgver.md" "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"

  # Desktop file
  install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/$_pkgname.desktop" <<EOF
[Desktop Entry]
Version=$pkgver
Type=Application
Name=$_PkgName
GenericName=$_PkgName
Comment=$pkgdesc
Exec=$_pkgname
Icon=$_pkgname
Terminal=false
Categories=Utility;Application;
Keywords=$_pkgname;anime
StartupNotify=true
EOF

}
