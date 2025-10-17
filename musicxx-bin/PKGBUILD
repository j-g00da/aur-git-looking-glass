# Maintainer: Coffee Bean <beanc904@gmail.com>
pkgname=musicxx-bin
_pkgname=musicxx
pkgver=0.81.7
pkgrel=1.0
pkgdesc="Audio and video player"
arch=(x86_64)
url="https://github.com/coolight7/musicxx"
_url="https://github.com/beanc904/musicxx-arch"
license=('MIT')
depends=('gtk3' 'util-linux' 'xz' 'mpv' 'ffmpeg' 'libkeybinder3' 'libayatana-appindicator' 'ayatana-ido')
install=.install
# source=("$_pkgname-$pkgver.tar.gz")
source=("${_pkgname}-${pkgver}.tar.gz::${_url}/releases/download/v${pkgver}/${_pkgname}-${pkgver}.tar.gz")
sha256sums=(d766905698fabb55d34d57224a7b5420854ce9b5e01c7a5047c4eb61b0b1683c)

package() {
  mkdir -p ${pkgdir}/opt
  install -Dm644 "${_pkgname}-${pkgver}/run.bool.musicxx.desktop" \
    "${pkgdir}/usr/share/applications/run.bool.musicxx.desktop"
  mv "${_pkgname}-${pkgver}" ${pkgdir}/opt/${_pkgname}
}

