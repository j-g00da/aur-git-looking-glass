# Maintainer: Yurii Kolesnykov <root@yurikoles.com>
# based on extra/xf86-video-ati by
# AndyRTR <andyrtr@archlinux.org>
#
# Pull requests are welcome here:
# https://github.com/yurikoles-aur/xf86-video-ati-git
#

pkgname=xf86-video-ati-git
pkgver=22.0.0.r12.g7fb27871
pkgrel=1
epoch=1
pkgdesc="X.org ati video driver"
arch=('x86_64')
url="https://xorg.freedesktop.org/"
license=('custom')
license=('MIT')
depends=('systemd-libs' 'mesa' 'libpciaccess' 'libdrm' 'glibc')
makedepends=('git' 'xorg-server-devel' 'systemd')
provides=("xf86-video-ati=${pkgver}")
conflicts=('xf86-video-ati')
groups=('xorg-drivers-git')
source=("${pkgname}::git+https://gitlab.freedesktop.org/xorg/driver/xf86-video-ati.git")
sha512sums=('SKIP')

pkgver() {
  cd ${pkgname}
  git describe --long | sed 's/^xf86-video-ati-//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd ${pkgname}
  NOCONFIGURE=1 ./autogen.sh
}

build() {
  cd ${pkgname}

#  CFLAGS+=' -fcommon' # https://wiki.gentoo.org/wiki/Gcc_10_porting_notes/fno_common

  # Since pacman 5.0.2-2, hardened flags are now enabled in makepkg.conf
  # With them, module fail to load with undefined symbol.
  # See https://bugs.archlinux.org/task/55102 / https://bugs.archlinux.org/task/54845
  export CFLAGS=${CFLAGS/-fno-plt}
  export CXXFLAGS=${CXXFLAGS/-fno-plt}
  export LDFLAGS=${LDFLAGS/-Wl,-z,now}

  ./configure --prefix=/usr
  make
}

check() {
  cd ${pkgname}
  make check
}

package() {
  cd ${pkgname}

  make "DESTDIR=${pkgdir}" install
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/"
}
