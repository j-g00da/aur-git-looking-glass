# Maintainer:  Vitalii Kuzhdin <vitaliikuzhdin@gmail.com>
# Maintainer:  artist for XLibre

_basename="xf86-video-intel"
pkgname="${_basename//xf86/xlibre}"
pkgver=3.0.0.4
pkgrel=1
pkgdesc="XLibre Intel i810/i830/i915/945G/G965+ video driver"
arch=('aarch64' 'x86_64')
url="https://github.com/X11Libre/${_basename}"
license=('MIT')
depends=('glibc' 'libpciaccess' 'libx11' 'libxcb' 'libxdamage' 'libdrm'
         'libxext' 'libxfixes' 'libxrender' 'libxshmfence' 'libxvmc' 'mesa'
         'pixman' 'systemd-libs' 'xcb-util>=0.3.9')
makedepends=('xlibre-server-devel' 'libxv' 'X-ABI-VIDEODRV_VERSION=28.0'
             # additional deps for intel-virtual-output
             'libxrandr' 'libxinerama' 'libxcursor' 'libxtst' 'libxss')
optdepends=('libxrandr: for intel-virtual-output'
            'libxinerama: for intel-virtual-output'
            'libxcursor: for intel-virtual-output'
            'libxtst: for intel-virtual-output'
            'libxss: for intel-virtual-output')
provides=("${_basename}" 'xf86-video-intel-uxa' 'xf86-video-intel-sna')
conflicts=("${_basename}" 'xf86-video-intel-uxa' 'xf86-video-intel-sna' 'xf86-video-i810' 'xf86-video-intel-legacy'
           'xorg-server<21.1.1' 'X-ABI-VIDEODRV_VERSION<28' 'X-ABI-VIDEODRV_VERSION>=29')
replaces=('xf86-video-intel-uxa' 'xf86-video-intel-sna')
groups=('xlibre-drivers')
options=('!lto')
_pkgsrc="${_basename}-xlibre-${_basename}-${pkgver}"
source=("${_pkgsrc}.tar.gz::${url}/archive/refs/tags/xlibre-${_basename}-${pkgver}.tar.gz")
b2sums=('0b696b27818d496bb8f73e5c2e46813552b493286e85be2b31239a69298a77bce6a0992eb0c5ce8b2d1136efd99202aec87a8ab077b0047092dce657b37a5512')

build() {
  # Since pacman 5.0.2-2, hardened flags are now enabled in makepkg.conf
  # With them, modules fail to load with undefined symbol.
  # See https://bugs.archlinux.org/task/55102 / https://bugs.archlinux.org/task/54845
  export CFLAGS="${CFLAGS/-fno-plt}"
  export CXXFLAGS="${CXXFLAGS/-fno-plt}"
  export LDFLAGS="${LDFLAGS/-Wl,-z,now}"
  local configure_options=(
    --prefix='/usr'
    --libexecdir='/usr/lib'
    --with-default-dri=3
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
