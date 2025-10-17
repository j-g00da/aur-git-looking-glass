# Maintainer:  Vitalii Kuzhdin <vitaliikuzhdin@gmail.com>
# Maintainer:  artist for XLibre

_basename="xf86-input-wacom"
pkgname="${_basename//xf86/xlibre}"
pkgver=1.2.3.1
pkgrel=2
pkgdesc="XLibre Wacom tablet driver"
arch=('aarch64' 'x86_64')
url="https://github.com/X11Libre/${_basename}"
license=('GPL-2.0-or-later')
depends=('glibc' 'libx11' 'libxi' 'libxinerama' 'libxrandr' 'systemd-libs')
makedepends=('gobject-introspection' 'meson>=0.51' 'python-libevdev' 'python-pytest'
             'python-yaml' 'python-gobject' 'python-attrs'
             'xlibre-xserver-devel' 'xorgproto' 'X-ABI-XINPUT_VERSION=26.0')
provides=("${_basename}")
conflicts=("${_basename}" 'xorg-server<21.1.1' 'X-ABI-XINPUT_VERSION<26' 'X-ABI-XINPUT_VERSION>=27')
groups=('xlibre-drivers')
_pkgsrc="${_basename}-xlibre-${_basename}-${pkgver}"
source=("${_pkgsrc}.tar.gz::${url}/archive/refs/tags/xlibre-${_basename}-${pkgver}.tar.gz")
b2sums=('dfb90ad5edfa5f1505be871fdd4c5055d3f324feb4f1ca3e4d89efc62a2e1f0df8e14edccbe780cf1c7431f07365727706d4dadae91cb7ec5376fb0d98bec807')

build() {
  export CFLAGS+=" -Wno-error=implicit-function-declaration"
  local meson_options=(
    "${_pkgsrc}"
    "${_pkgsrc}/build"
    -D xorg-conf-dir='/usr/share/X11/xorg.conf.d'
    -D systemd-unit-dir='/usr/lib/systemd/system'
    -D unittests=enabled
  )

  cd "${srcdir}"
  arch-meson "${meson_options[@]}"
  meson compile -C "${_pkgsrc}/build"
}

check() {
  cd "${srcdir}"
  meson test -C "${_pkgsrc}/build"
}

package() {
  cd "${srcdir}"
  meson install -C "${_pkgsrc}/build" --destdir "${pkgdir}"

  cd "${_pkgsrc}"
  install -vDm644 "README.md" "${pkgdir}/usr/share/doc/${pkgname}/README.md"
  install -vDm644 "GPL"       "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
