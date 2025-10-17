# Maintainer: Xesxen <arch@xesxen.nl>
# Contributor: Gaetan Bisson <bisson@archlinux.org>

pkgname=vvvvvv-archipelago-git
binname=vvvvvv-archipelago
pkgver=20250412.027daa5d
_pkgver=git
pkgrel=2
pkgdesc='A retro-styled 2D platformer patched for Archipelago multiworld'
arch=('i686' 'x86_64')
url='https://github.com/peppidesu/vvvvvv-archipelago-git.git'
license=('custom')
depends=('sh' 'sdl2_mixer')
makedepends=('git' 'cmake')
provides=('vvvvvv-archipelago')
conflicts=('vvvvvv-archipelago')
source=(
  "git+https://github.com/N00byKing/VVVVVV"
  "git+https://github.com/lvandeve/lodepng"
  "git+https://github.com/icculus/physfs/"
  "git+https://github.com/leethomason/tinyxml2/"
  "git+https://github.com/FNA-XNA/FAudio"
  "git+https://github.com/Mashpoe/c-hashmap"
  "git+https://github.com/N00byKing/APCpp"
  "git+https://github.com/Tehreer/SheenBidi"
  "git+https://github.com/machinezone/IXWebSocket"
  "git+https://github.com/open-source-parsers/jsoncpp"
  "git+https://github.com/madler/zlib"
  "${binname}.sh"
)
sha256sums=('SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  '0c0d10f1a64a5c3bf703af38cb0f79fa7b77fb7f43e8eec9a906da454f1e34d1'
)
install=${pkgname}.install

pkgver() {
  cd "${srcdir}/VVVVVV"
  git log -1 --format='%cd.%h' --date=short | tr -d -
}

prepare() {
  cd VVVVVV
  git submodule init
  for submodule in lodepng physfs tinyxml2 FAudio c-hashmap APCpp SheenBidi; do
    git config "submodule.third_party/$submodule.url" "$srcdir/$submodule"
  done
  git -c protocol.allow=never -c protocol.file.allow=always submodule update

  cd "third_party/APCpp"
  for submodule in IXWebSocket jsoncpp zlib; do
    git config "submodule.$submodule.url" "$srcdir/$submodule"
  done
  git -c protocol.allow=never -c protocol.file.allow=always submodule update
}

build() {
  cd VVVVVV/desktop_version
  mkdir -p build
  cd build
  cmake ..
  make
}

package() {
  cd "${srcdir}/VVVVVV/desktop_version/build"
  install -d "${pkgdir}/opt/${binname}"
  install -D -m644 ../../LICENSE.md "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
  # Legal: There used to be a separate LICENSE-data.md, but the LICENSE.md also mentions the "Make and Play" edition specifically.
  # We now instead warn the user on build they should not redistribute the package and mention the same on install
  install -m755 "VVVVVV" \
    "${pkgdir}/opt/${binname}/${binname}"

  cd "${srcdir}"
  install -D -m755 "${srcdir}/${binname}.sh" "${pkgdir}/usr/bin/${binname}"
}
