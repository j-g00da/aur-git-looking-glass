# Maintainer: Nihal Kumar <2tv8xupqg at mozmail dot com>

pkgname=twitter-media-downloader-bin
_pkgname=twitter-media-downloader
pkgver=1.14.2
pkgrel=1
pkgdesc="A tool to download media from Twitter (pre-built binary)"
arch=('x86_64' 'aarch64')
url="https://github.com/mmpx12/twitter-media-downloader"
license=('unknown')
depends=('glibc')
provides=("${_pkgname}")
conflicts=("${_pkgname}" "${_pkgname}-git")
source_x86_64=("https://github.com/mmpx12/${_pkgname}/releases/download/v${pkgver}/${_pkgname}-v${pkgver}-linux-amd64.tar.gz")
source_aarch64=("https://github.com/mmpx12/${_pkgname}/releases/download/v${pkgver}/${_pkgname}-v${pkgver}-linux-arm64.tar.gz")
sha256sums_x86_64=('52c306a32db7e78a054d21c742f3b0b04baff9d5fef6fd16992929a678fb79b9')
sha256sums_aarch64=('3432adb63bd80f924ce24a092d44d2e40df33797b743356e71bd49a2a1eab45b')

package() {
  install -Dm755 "${srcdir}/twitter-media-downloader" "${pkgdir}/usr/bin/twmd"
}
