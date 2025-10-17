# Maintainer: Pfych <contact at pfy dot ch>
pkgname=lr2oraja-endlessdream
pkgver=0.3.0
_basever=0.8.8
pkgrel=6
url="https://github.com/seraxis/lr2oraja-endlessdream"
pkgdesc="A featureful fork of beatoraja."
arch=('x86_64')
depends=('bash' 'liberica-jdk-17-full-bin')
makedepends=('unzip' 'git' 'cmake' 'gcc')
_portaudio_java_commit="2ec5cc47d6f8abe85ddb09c34e69342bfe72c60b"
source=(
  "https://github.com/seraxis/lr2oraja-endlessdream/releases/download/v${pkgver}/lr2oraja-${_basever}-endlessdream-linux-${pkgver}.jar"
  "https://github.com/philburk/portaudio-java/archive/${_portaudio_java_commit}.tar.gz"
  'https://github.com/zkrising/tachi-beatoraja-ir/releases/download/v3.1.0/bokutachiIR-3.1.0.jar'
  'lr2oraja-endlessdream.sh'
  'lr2oraja-endlessdream-icon.png'
  'lr2oraja-endlessdream.desktop'
)
sha256sums=(
  'c77719e5be5f650755297e837f8e26df998662d066334153c63e219bc03a851d' # lr2oraja-endlessdream.jar
  '7a70d90d449fc9d91026c54e1d08303242749475ad20b30b5bfa45fc93f18043' # philburk/portaudio-java
  '11d0069581c81026aa016cf5452c7fd3c1812d220b827b0674ebfa1bbbaaeb83' # bokutachiIR
  '0246f27a70159da8a068e9613cd6d858e6dd546acde5e58ee93e564e5af5f5f5' # lr2oraja-endlessdream.sh
  'fdbd37ff43aa6af20f9eb643bf271a77ef579014970a7a3dcecf78e65123d83d' # lr2oraja-endlessdream-icon.png
  '8ad578f30b046fd35b4f412dcb2c9039a8b9a3ebfd5e8299328b92234f4c9901' # lr2oraja-endlessdream.desktop
)
license=(
  'GPL3'
  'GPL3'
  'MIT'
)
install=migrate.install

prepare() {
  # Fetch for required game assets
  git clone --depth 1 --branch "v${pkgver}" "https://github.com/seraxis/lr2oraja-endlessdream" upstream
}

build() {
  # Build native dependencies
export JAVA_HOME=/usr/lib/jvm/liberica-jdk-17-full
  cd "${srcdir}/portaudio-java-${_portaudio_java_commit}"
  cmake -DCMAKE_POLICY_VERSION_MINIMUM=3.5 .
  cmake --build .
}

package() {
  cd "$srcdir/"

  # Move Assets
  install -dm755 "${pkgdir}/usr/share/${pkgname}"
  cp -r upstream/assets/* "${pkgdir}/usr/share/${pkgname}"
  rm -f "${pkgdir}/usr/share/${pkgname}"/beatoraja-config*

  # Bokutachi IR
  mkdir -p "${pkgdir}/usr/share/${pkgname}/ir/"
  cp "bokutachiIR-3.1.0.jar" "${pkgdir}/usr/share/${pkgname}/ir/"

  # Portaudio-java native library
  install -Dm644 "${srcdir}/portaudio-java-${_portaudio_java_commit}/libjportaudio_0_1_0.so" \
      "${pkgdir}/usr/share/${pkgname}/natives/libjportaudio.so"

  # Desktop icon
  install -Dm644 lr2oraja-endlessdream-icon.png "$pkgdir/usr/share/pixmaps/lr2oraja-endlessdream-icon.png"

  # Desktop entry
  install -Dm644 lr2oraja-endlessdream.desktop "$pkgdir/usr/share/applications/lr2oraja-endlessdream.desktop"
  sed -i "s/__PKGVER__/${pkgver}/" \
      "${pkgdir}/usr/share/applications/lr2oraja-endlessdream.desktop"

  # Game executable
  install -Dm644 "lr2oraja-${_basever}-endlessdream-linux-${pkgver}.jar" "${pkgdir}/usr/share/${pkgname}/LR2oraja-endlessdream.jar"

  # Launcher script
  install -Dm755 lr2oraja-endlessdream.sh "$pkgdir/usr/bin/lr2oraja-endlessdream"

  # Create symlink
  if [ -z "$XDG_CONFIG_HOME" ]; then
    XDG_CONFIG_HOME="$HOME/.config"
  fi
  ln -sfn "/usr/share/${pkgname}" "$XDG_CONFIG_HOME/lr2oraja-endlessdream"

  # Allow install modification
  chmod -R 777 "${pkgdir}/usr/share/${pkgname}"
}
