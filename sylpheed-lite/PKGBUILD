# Contributor: Lex Black <autumn-wind at web dot de>
# Contributor: Westminboy <westminboy@gmail.com>

pkgname=sylpheed-lite
_pkgname=sylpheed
pkgver=3.8.0beta1
pkgrel=1
pkgdesc="Lightweight in lightweight and user-friendly e-mail client"
arch=('i686' 'x86_64')
url="https://sylpheed.sraoss.jp/en/"
license=('GPL')
depends=('gtk2' 'gpgme' 'desktop-file-utils')
makedepends=('openssl')
options=('!libtool')
conflicts=('sylpheed')
source=("https://sylpheed.sraoss.jp/$_pkgname/v${pkgver%.*}beta/$_pkgname-$pkgver.tar.gz"
        "https://sylpheed.sraoss.jp/$_pkgname/v${pkgver%.*}beta/$_pkgname-$pkgver.tar.gz.asc"
        "0013-fix-FTBFS-GCC-14.patch")
validpgpkeys=('8CF3A5AC417ADE72B0AA4A835024337CC00C2E26') # Hiroyuki Yamamoto
sha256sums=('d14a90e9950187eb0e184a08461bd9dc4b66a4587f4b6a7e14e8d6b97e4143f0'
            'SKIP'
            'b2716999fcf95037460c18dfdbe7350a182b9e9a834d8d996a0b111d7df2ce30')

prepare() {
  cd "$_pkgname-$pkgver"
  patch -Np1 -i "${srcdir}/0013-fix-FTBFS-GCC-14.patch"
}

build() {
  cd "$_pkgname-$pkgver"

  # Change incompatible-pointer-type back to warning instead of error (default GCC 14+)
  CFLAGS+=' -Wno-error=incompatible-pointer-types'

  ./configure --prefix=/usr \
    --disable-compface \
    --disable-gtkspell \
    --disable-ipv6 \
    --disable-updatecheck
  make

  # Build Attachment-Tool Plug-in
  cd plugin/attachment_tool && make
}

package() {
  cd "$_pkgname-$pkgver"
  make DESTDIR="$pkgdir/" install

  # Install Attachment-Tool Plug-in
  cd plugin/attachment_tool
  make DESTDIR="$pkgdir/" install-plugin
}
