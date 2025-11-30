# Maintainer: Jason Go <jasongo@jasongo.net>
# Contributor: Taboon Egon <te451 -_AT_- netcourrier -_DOT_- com>
# Contributor: relrel <relrelbachar at gmail dot com>

pkgname="scratch3"
pkgver=3.31.1
pkgrel=3
pkgdesc='Scratch 3.0 as a self-contained desktop application'
arch=('x86_64' 'aarch64')
url='https://github.com/scratchfoundation/scratch-desktop'
license=('AGPL-3.0-only')
depends=('fuse2')
makedepends=('git' 'nodejs' 'npm')
provides=('scratch3')
conflicts=('scratch3-bin' 'scratch-desktop')
replaces=('scratch-desktop')
options=(!strip !debug)
source=("git+$url.git#tag=v$pkgver"
        "$pkgname.desktop"
        "$pkgname.xml")
sha256sums=('e38d5e8febfd61454d5d4f402177963deedc8350a37ee4dd327cd5079614d4eb'
            '0f4f25e55b988e45a2f240487c35b18c96bbbce0f6be60bbe204b33f6d77d6da'
            '86c8e16d9316dcbe21c19928381a498f5198708cae0ed25bfa3c09371d02deaf')

prepare() {
  cd scratch-desktop

  # Patch: Set window icon
  sed -i "s#const window = new BrowserWindow({#const window = new BrowserWindow({ icon: '/usr/share/icons/hicolor/1024x1024/apps/scratch3.png',#g" ./src/main/index.js
  
  npm install
  npm run clean
  npm run fetch
}

build() {
  cd scratch-desktop
  npm run build:dist
}

package() {
  install -Dm755 "$srcdir/scratch-desktop/dist/Scratch 3-$pkgver.AppImage" "$pkgdir/usr/bin/scratch3"
  install -Dm644 "$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
  install -Dm644 "$srcdir/scratch-desktop/src/icon/ScratchDesktop.png" "$pkgdir/usr/share/icons/hicolor/1024x1024/apps/$pkgname.png"
  install -Dm644 "$srcdir/scratch-desktop/src/icon/ScratchDesktop.svg" "$pkgdir/usr/share/icons/hicolor/scalable/apps/$pkgname.svg"
  install -Dm644 "$srcdir/scratch-desktop/src/icon/ScratchDesktop.svg" "$pkgdir/usr/share/icons/hicolor/scalable/mimetypes/x-scratch3-project.svg"
  install -Dm644 "$srcdir/scratch-desktop/src/icon/ScratchDesktop.svg" "$pkgdir/usr/share/icons/hicolor/scalable/mimetypes/x-scratch3-sprite.svg"
  install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" "$srcdir/scratch-desktop/"{LICENSE,TRADEMARK}
}
