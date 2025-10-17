# Maintainer:  Vitalii Kuzhdin <vitaliikuzhdin@gmail.com>
# Maintainer:  artist for XLibre

_basename="xf86-input-vmmouse"
pkgname="${_basename//xf86/xlibre}"
pkgver=13.2.0.2
pkgrel=1
pkgdesc="XLibre VMWare Mouse input driver"
arch=('aarch64' 'x86_64')
url="https://github.com/X11Libre/${_basename}"
license=('custom')
depends=('glibc' 'systemd-libs')
makedepends=('xlibre-xserver-devel' 'xorgproto' 'X-ABI-XINPUT_VERSION=26.0')
provides=("${_basename}")
conflicts=("${_basename}" 'xorg-server<21.1.1' 'X-ABI-XINPUT_VERSION<26' 'X-ABI-XINPUT_VERSION>=27')
groups=('xlibre-drivers')
_pkgsrc="${_basename}-xlibre-${_basename}-${pkgver}"
source=("${_pkgsrc}.tar.gz::${url}/archive/refs/tags/xlibre-${_basename}-${pkgver}.tar.gz")
b2sums=('0ed37d5583f566eb72627a369b31336a5d55ffe10e33ef547541223190eb95e29c95dc006c20c3a31d532f98f10056e5958fd82dec50a84d3dd91a4a82283d99')

build() {
  local configure_options=(
    --prefix='/usr'
    --with-udev-rules-dir='/usr/lib/udev/rules.d'
  )

  cd "${srcdir}/${_pkgsrc}"
  autoreconf -vfi
  ./configure "${configure_options[@]}"
  make
}

package() {
  cd "${srcdir}/${_pkgsrc}"
  make DESTDIR="${pkgdir}" install

  install -vDm644 "README"  "${pkgdir}/usr/share/doc/${pkgname}/README"
  install -vDm644 "COPYING" "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
