# Maintainer: Phil A. <flying-sheep@web.de>

pkgname=twemoji-mozilla-fontconfig
pkgver=1.0
pkgrel=1
pkgdesc="Use Mozilla version of Twitter Color Emoji."
url="https://github.com/mozilla/twemoji-colr"
arch=(any)
license=('Apache-2.0 AND CC-BY-4.0')
dependencies=('firefox')
provides=('emoji-font' 'twemoji-color-font')
source=("75-twemoji-mozilla.conf" "$url/blob/master/LICENSE.md")
sha256sums=('fd46c9e90c73a8516934515128230f4decf7300e12174f220c890d5f1801340c'
            'SKIP')

package() {
  install -dm755 "$pkgdir/usr/share/fonts/twemoji-mozilla"
  ln -s "/usr/lib/firefox/fonts/TwemojiMozilla.ttf" \
    "$pkgdir/usr/share/fonts/twemoji-mozilla/"
  install -Dm644 -t "$pkgdir/usr/share/fontconfig/conf.d" "$srcdir/75-twemoji-mozilla.conf"
  install -Dm644 -t "$pkgdir/usr/share/licenses/$pkgname" "$srcdir/LICENSE.md"
}
