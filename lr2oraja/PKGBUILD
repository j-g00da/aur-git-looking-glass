# Maintainer: Pfych <contact at pfy dot ch>
pkgname=lr2oraja
pkgver=build11611350155
pkgrel=5
pkgdesc="The latest build of beatoraja, but compiled using LR2 judges and gauges."
arch=('x86_64')
depends=('liberica-jdk-17-full-bin' 'portaudio')
makedepends=('unzip')
source=(
  "https://github.com/wcko87/lr2oraja/releases/download/${pkgver}/LR2oraja.zip"
  'https://github.com/pfych/lr2oraja-pkgbuild/releases/download/skin/skin.zip'
  'https://github.com/zkrising/tachi-beatoraja-ir/releases/download/v3.1.0/bokutachiIR-3.1.0.jar'
  'libjportaudio.so'
  'beatoraja.sh'
  'lr2oraja-icon.png'
)
sha256sums=(
  '3cdbe4ecabd7937003fc721cd2eb53af88e52881fc4920480526df6d70b9932b' # LR2oraja.zip
  'ef23b516537b4f52c306fd61ab9c4197192c06b7202b3b27b63481fec1042a26' # skin.zip
  '11d0069581c81026aa016cf5452c7fd3c1812d220b827b0674ebfa1bbbaaeb83' # bokutachiIR
  'a65d1290d3ee7710f9327c040e6369bf7587eb3609835ed782caaf0ac02d84ed' # libjportaudio.so
  '2d8dffe53a24fd5df6198ee30a4473129cfbeb3e7a6c8f1e70535a19a871b3e8' # beatoraja.sh
  '0ec1382690cd847055d1b8e6da36ad6846598b45b25acca5eb5e301a5048da03' # lr2oraja-icon.png
)
license=(
  'GPL3'
  'GPL3'
  'MIT'
  'unknown'
  'unknown'
)

prepare() {
  # Beatoraja will fail to load without a default skin
  unzip -o skin.zip
}

build() {
  unzip -o LR2oraja.zip
}

package() {
  # Create required directories
  cd "$srcdir/"
  mkdir -p "$pkgdir/opt/beatoraja/ir"
  mkdir -p "$pkgdir/usr/lib"
  mkdir -p "$pkgdir/usr/share/applications"
  mkdir -p "$pkgdir/usr/share/pixmaps"

  # Move all required Beatoraja Files
  cp libjportaudio.so "$pkgdir/usr/lib"
  cp beatoraja.jar "$pkgdir/opt/beatoraja/beatoraja.jar"
  cp -r skin "$pkgdir/opt/beatoraja"
  cp "bokutachiIR-3.1.0.jar" "$pkgdir/opt/beatoraja/ir"
  chmod -R 777 "$pkgdir/opt/beatoraja"

  # Create Desktop entry
  cp lr2oraja-icon.png "$pkgdir/usr/share/pixmaps"
  desktopEntry="$pkgdir/usr/share/applications/lr2oraja.desktop"
  touch "$desktopEntry"
  echo "[Desktop Entry]" >>"$desktopEntry"
  echo "Type=Application" >>"$desktopEntry"
  echo "Terminal=true" >>"$desktopEntry"
  echo "Exec=/usr/bin/beatoraja" >>"$desktopEntry"
  echo "Version=$pkgver" >>"$desktopEntry"
  echo "Name=LR2oraja" >>"$desktopEntry"
  echo "Categories=Game;" >>"$desktopEntry"
  echo "Icon=lr2oraja-icon" >>"$desktopEntry"

  if [ -z "$XDG_CONFIG_HOME" ]; then
    XDG_CONFIG_HOME="$HOME/.config"
  fi

  # Create config symlink
  ln -sfn "/opt/beatoraja" "$XDG_CONFIG_HOME/beatoraja"

  # Install LR2oraja
  install -D beatoraja.sh "$pkgdir/usr/bin/beatoraja"
}
