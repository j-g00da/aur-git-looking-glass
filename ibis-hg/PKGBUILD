# Maintainer: Solomon Choina <shlomochoina@gmail.com>
_pkgbase=ibis
pkgbase=ibis-hg
pkgname=("$_pkgbase-hg" "$_pkgbase-docs-hg")
pkgver=206.6fc6490ebc08
pkgrel=1
pkgdesc="A GObjects based IRCv3 library."
arch=('i686' 'x86_64' 'armv7h')
url="https://keep.imfreedom.org/xeme/xeme/"
license=('LGPL-2.1-or-later')
depends=('glib2' 'hasl-hg' 'pango')
makedepends=('mercurial' 'meson' 'help2man' 'vala' 'gi-docgen' 'gobject-introspection' 'birb-hg')
source=("hg+https://keep.imfreedom.org/ibis/ibis#branch=default")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgbase"

  hg identify -ni | awk 'BEGIN{OFS=".";} {print $2,$1}'
}

_pick() {
  local p="$1" f d; shift
  for f; do
    d="$srcdir/$p/${f#$pkgdir/}"
    mkdir -p "$(dirname "$d")"
    mv "$f" "$d"
    rmdir -p --ignore-fail-on-non-empty "$(dirname "$f")"
  done
}

build() {
  arch-meson ibis build
  ninja -C build
}

package_ibis-hg() {
  depends+=(birb-hg)
  provides=(ibis)
  DESTDIR="$pkgdir" ninja -C build install
 cd $pkgdir
 _pick docs usr/share/doc
}

package_ibis-docs-hg() {
  pkgdesc+=" (documentation)"
  provides=(ibis-docs)
  depends=()
  mv docs/* "$pkgdir"


}
