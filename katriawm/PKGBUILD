# Contributor: Lex Black <autumn-wind@web.de>
# Contributor: Tmplt <tmplt@dragons.rocks>

pkgname=katriawm
pkgver=25.09
pkgrel=1
pkgdesc="non-reparenting, dynamic window manager for X11 with decorations"
arch=("i686" "x86_64")
url="https://www.uninformativ.de/git/katriawm/file/README.html"
license=("MIT")
makedepends=("git")
depends=("libx11" "libxft" "libxrandr")
source=("git+https://www.uninformativ.de/git/katriawm.git#tag=v${pkgver}")
sha256sums=('768e36cd146ff494b828219d43f20fe62ecfb2edddc5df8b11a146561cc708a6')


prepare() {
  cd "${pkgname}/src"

  # Read custom config headers from $XDG_CONFIG_HOME/katria{wm,bi}-config.h
  config=${XDG_CONFIG_HOME:-~/.config/}

  if [[ -f "${config}/katriawm-config.h" ]]; then
      msg "Using custom config.h for katriawm(1)"
      cp -f "${config}/katriawm-config.h" core/config.h
  fi

  if [[ -f "${config}/katriabi-config.h" ]]; then
      msg "Using custom config.h for katriabi(1)"
      cp -f "${config}/katriabi-config.h" barinfo/config.h
  fi
}

build() {
  cd "${pkgname}/src"
  make prefix=/usr
}

package() {
  cd "${pkgname}/src"
  make prefix=/usr DESTDIR=${pkgdir} install
  install -Dm644 ../LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
