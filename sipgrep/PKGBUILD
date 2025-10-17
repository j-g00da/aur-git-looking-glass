# Maintainer:  Andrew O'Neill <andrew at haunted dot sh>
# Contributor: Andrew Sun <adsun701 at gmail dot com>
# Contributor: Xavier Devlamynck <magicrhesus at ouranos dot be>

pkgname=sipgrep
pkgver=2.2.0
pkgrel=2
pkgdesc='A powerful pcap-aware tool command line tool to sniff, capture, display and troubleshoot SIP signaling over IP networks'
arch=('x86_64')
url="https://github.com/sipcapture/${pkgname}"
license=('GPL-3.0-only')
depends=('pcre' 'libpcap')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/${pkgver}.tar.gz")
sha256sums=('ee16c1efde73c8faa591f8d84b697b629fabf43806fb292893a3ba3f8cc9a290')

build() {
  cd "${pkgname}-${pkgver}"

  sed -i '22i #include <arpa/inet.h>' src/transport_hep.c
  sed -i 's/AC_INIT(sipgrep,2.2.1/AC_INIT(sipgrep,2.2.0/' configure.ac
  export CFLAGS="-std=gnu17" 
  ./build.sh
  ./configure --prefix=/usr --enable-ipv6
  make
}

package() {
  cd "${pkgname}-${pkgver}"

  make DESTDIR="${pkgdir}" install
  install -Dm644 sipgrep.8 "${pkgdir}/usr/share/man/man8/sipgrep.8"
}
