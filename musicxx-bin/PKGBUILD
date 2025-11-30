# Maintainer: Coffee Bean <beanc904@gmail.com>
pkgname=musicxx-bin
_pkgname=musicxx
pkgver=0.82.7
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
sha256sums=(ef739b7a7e4515c2cc4130fb5fa6f6a2568a2ddb1824c046831b1e79bde9b1ea)

package() {
  mkdir -p ${pkgdir}/opt
  install -Dm644 "${_pkgname}-${pkgver}/run.bool.musicxx.desktop" \
    "${pkgdir}/usr/share/applications/run.bool.musicxx.desktop"
  mv "${_pkgname}-${pkgver}" ${pkgdir}/opt/${_pkgname}
}

