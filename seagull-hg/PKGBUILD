# Maintainer: Solomon Choina <shlomochoina@gmail.com>
_pkgbase=seagull
pkgbase=seagull-hg
pkgname=("$_pkgbase-hg" "$_pkgbase-docs-hg")
pkgver=46.c5102bd9161a
pkgrel=1
pkgdesc="GObject based SQLite helper library."
arch=('i686' 'x86_64' 'armv7h')
url="https://keep.imfreedom.org/seagull/seagull/"
license=('GPL-2.0-or-later')
depends=('glib2')
makedepends=('mercurial' 'meson' 'help2man' 'vala' 'gi-docgen' 'gobject-introspection' 'sqlite')
source=("hg+https://keep.imfreedom.org/seagull/seagull#branch=default")
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
  arch-meson seagull build
  ninja -C build
}

package_seagull-hg() {
  depends+=()
  DESTDIR="$pkgdir" ninja -C build install
 cd $pkgdir
 _pick docs usr/share/doc
}

package_seagull-docs-hg() {
  pkgdesc+=" (documentation)"
  depends=()
  mv docs/* "$pkgdir"


}
