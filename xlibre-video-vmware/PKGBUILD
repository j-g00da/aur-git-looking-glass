# Maintainer:  artist for XLibre
# Maintainer:  Vitalii Kuzhdin <vitaliikuzhdin@gmail.com>

_basename="xf86-video-vmware"
pkgname="${_basename//xf86/xlibre}"
pkgver=13.4.0.3
pkgrel=1
pkgdesc="XLibre vmware video driver"
arch=('aarch64' 'x86_64')
url="https://github.com/X11Libre/${_basename}"
license=('MIT AND X11')
depends=('mesa' 'systemd-libs' 'libxext' 'libx11' 'libdrm' 'glibc')
makedepends=('xlibre-xserver-devel' 'xorgproto' 'X-ABI-VIDEODRV_VERSION=28.0')
provides=("${_basename}")
conflicts=("${_basename}" 'xorg-server<1.20.0' 'X-ABI-VIDEODRV_VERSION<28' 'X-ABI-VIDEODRV_VERSION>=29')
groups=('xlibre-drivers')
options=('!emptydirs' '!debug')
_pkgsrc="${_basename}-xlibre-${_basename}-${pkgver}"
source=("${_pkgsrc}.tar.gz::${url}/archive/refs/tags/xlibre-${_basename}-${pkgver}.tar.gz")
b2sums=('a8aec38a07d4ab6de7c3d072ca83900c1884055d1a2ea237cb12a3cf9800dfebf398d0fdf387c287ed21636035281499bb7c0c2de058e98eda6b1a1cd08a196b')

build() {
  # Since pacman 5.0.2-2, hardened flags are now enabled in makepkg.conf
  # With them, modules fail to load with undefined symbol.
  # See https://bugs.archlinux.org/task/55102 / https://bugs.archlinux.org/task/54845
  export CFLAGS="${CFLAGS/-fno-plt}"
  export CXXFLAGS="${CXXFLAGS/-fno-plt}"
  export LDFLAGS="${LDFLAGS/-Wl,-z,now}"
  local configure_options=(
    --prefix='/usr'
  )

  cd "${srcdir}/${_pkgsrc}"
  autoreconf -vfi
  ./configure "${configure_options[@]}"
  make
}

package() {
  cd "${srcdir}/${_pkgsrc}"
  make DESTDIR="${pkgdir}" install

  install -vDm644 "README" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -vDm644 "COPYING"   "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
