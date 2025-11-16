# Maintainer: artist for XLibre <artist4xlibre@proton.me>

_basename="xf86-input-vmmouse"
pkgname="${_basename//xf86/xlibre}"
pkgver=13.2.0.3
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
b2sums=('bc34c05fc910fe58515a4bf9f113a033a198e45b69d0b1af27b4f0b909e4ffd750e211148790872afe30595391f379fa15cec243b18a0bc701cb09a8c3df2f8c')

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
