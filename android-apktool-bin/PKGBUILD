# Maintainer: bemxio <bemxiov at protonmail dot com>
# Maintainer: Joseph Brains <jnbrains at gmail dot com>

_pkgname=android-apktool
pkgname=${_pkgname}-bin

pkgdesc="A tool for reverse engineering Android .apk files"

pkgver=2.12.1
pkgrel=1

arch=(any)

url="https://github.com/iBotPeaches/Apktool"
license=("Apache-2.0")

depends=("java-runtime>=8")

provides=("${_pkgname}")
conflicts=("${_pkgname}" "${_pkgname}-git")

source=("https://github.com/iBotPeaches/Apktool/releases/download/v${pkgver}/apktool_${pkgver}.jar"
  "apktool")
sha256sums=('66cf4524a4a45a7f56567d08b2c9b6ec237bcdd78cee69fd4a59c8a0243aeafa'
  '48a5c9d664c88c8beac4a85461e84437d104a42dac6334322a3bafca12b63bae')

noextract=("apktool_${pkgver}.jar")

package() {
  # copy the main .jar file
  install -Dm644 "apktool_${pkgver}.jar" "${pkgdir}/usr/share/java/${_pkgname}/apktool.jar"

  # copy the executable script
  install -Dm755 apktool "${pkgdir}/usr/bin/apktool"
}
