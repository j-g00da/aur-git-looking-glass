# Maintainer:  Vitalii Kuzhdin <vitaliikuzhdin@gmail.com>
# Maintainer:  artist for XLibre

_basename="xf86-video-qxl"
pkgname="${_basename//xf86/xlibre}"
pkgver=0.1.6.1
pkgrel=2
pkgdesc="XLibre qxl video driver"
arch=('aarch64' 'x86_64')
url="https://github.com/X11Libre/${_basename}"
license=('MIT')
depends=('glibc' 'libxfont2' 'spice' 'systemd-libs')
makedepends=('libcacard' 'spice-protocol' 'xlibre-xserver-devel' 'xorgproto' 'X-ABI-VIDEODRV_VERSION=28.0')
optdepends=('python: for Xspice')
provides=("${_basename}")
conflicts=("${_basename}" 'xorg-server<1.20.0' 'X-ABI-VIDEODRV_VERSION<28' 'X-ABI-VIDEODRV_VERSION>=29')
groups=('xlibre-drivers')
_pkgsrc="${_basename}-xlibre-${_basename}-${pkgver}"
source=("${_pkgsrc}.tar.gz::${url}/archive/refs/tags/xlibre-${_basename}-${pkgver}.tar.gz")
b2sums=('2bb739ca8171b73069d1d1d7a3d5e247fbf954e01db714b88fd89dd16e5fa6f4e7adf071d29f8d36f5f39d3bde970ff6221b99dde49fea3c2f41c82981fe10f9')

build() {
  # Since pacman 5.0.2-2, hardened flags are now enabled in makepkg.conf
  # With them, modules fail to load with undefined symbol.
  # See https://bugs.archlinux.org/task/55102 / https://bugs.archlinux.org/task/54845
  export CFLAGS="${CFLAGS/-fno-plt}"
  export CXXFLAGS="${CXXFLAGS/-fno-plt}"
  export LDFLAGS="${LDFLAGS/-Wl,-z,now}"
  local configure_options=(
    --prefix='/usr'
    --enable-xspice
  )

  cd "${srcdir}/${_pkgsrc}"
  autoreconf -vfi
  ./configure "${configure_options[@]}"
  make
}

package() {
  cd "${srcdir}/${_pkgsrc}"
  make DESTDIR="${pkgdir}" install

  install -vDm755 scripts/Xspice "${pkgdir}"/usr/bin/Xspice
  install -vDm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -vDm644 "COPYING"   "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
