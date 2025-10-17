# Maintainer: Michael Engelhard <engelhard.michael+git@gmail.com>
pkgname=neolight
pkgver=1.4.0
pkgrel=1
pkgdesc='Additional layers for the german qwertz keyboard layout and others.'
arch=('any')
url='https://github.com/mihi314/neolight'
license=('GPL-3.0-or-later')
depends=('xkeyboard-config')
optdepends=('ibus: adds neolight to the ibus input methods')

_tag="v${pkgver}"
_repo_url='https://raw.githubusercontent.com/mihi314/neolight'

install='neolight.install'
# TODO: maybe release a tarball instead of specifying individual files here
source=("neolight_symbols-${pkgver}::${_repo_url}/${_tag}/linux/neolight_symbols"
        "neolight_types-${pkgver}::${_repo_url}/${_tag}/linux/neolight_types"
        "register-neolight.sh-${pkgver}::${_repo_url}/${_tag}/linux/register-neolight.sh"
        "find-xkeyboard-config-dir.sh-${pkgver}::${_repo_url}/${_tag}/linux/find-xkeyboard-config-dir.sh"
        "register-neolight.hook")
md5sums=('e3cf94066cf6ee04a973f213fefb7f18'
         'ba64578baee9718f00f989cf8025ea0a'
         '44e4940cf7115c4d7ed169346754845b'
         '7276c6fce6cbdc5cba9e28073723e273'
         '828a62be3f8288ea9f73a95934ebd1a0')

package() {
    install -Dm 644 "${srcdir}/neolight_symbols-${pkgver}" "${pkgdir}/usr/share/xkeyboard-config-2/symbols/neolight"
    install -Dm 644 "${srcdir}/neolight_types-${pkgver}" "${pkgdir}/usr/share/xkeyboard-config-2/types/neolight"
    install -Dm 755 "${srcdir}/register-neolight.sh-${pkgver}" "${pkgdir}/usr/share/libalpm/scripts/register-neolight.sh"
    install -Dm 755 "${srcdir}/find-xkeyboard-config-dir.sh-${pkgver}" "${pkgdir}/usr/share/libalpm/scripts/find-xkeyboard-config-dir.sh"
    install -Dm 644 "${srcdir}/register-neolight.hook" "${pkgdir}/usr/share/libalpm/hooks/register-neolight.hook"
}
