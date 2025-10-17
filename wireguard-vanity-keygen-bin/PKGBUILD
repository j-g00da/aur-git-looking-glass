# Maintainer: Winston Astrachan <winston dot astrachan at gmail dot com>

pkgname=wireguard-vanity-keygen-bin
_shortname=wireguard-vanity-keygen
pkgver=0.1.1
pkgrel=2
pkgdesc='WireGuard vanity key generator'
arch=('x86_64' 'aarch64' 'i686' 'arm')
url='https://github.com/axllent/wireguard-vanity-keygen'
license=('MIT')
depends=('glibc')
provides=("${_shortname}")
conflicts=("${_shortname}")
_source_url="https://github.com/axllent/wireguard-vanity-keygen"
_download_path="${_source_url}/releases/download/${pkgver}"
source_x86_64=("${_download_path}/${_shortname}-linux-amd64.tar.gz")
source_aarch64=("${_download_path}/${_shortname}-linux-arm64.tar.gz")
source_i686=("${_download_path}/${_shortname}-linux-386.tar.gz")
source_arm=("${_download_path}/${_shortname}-linux-arm.tar.gz")
sha256sums_x86_64=('9a092217fb7419402071db92ab6c4fb5a7ab8972c2b273733c75517d3b86d2c4')
sha256sums_aarch64=('71476b987cf37047ee449d06864c61926519746a93f71755bd5bb450dcd94bfa')
sha256sums_i686=('694813431dbe0bced13d03257a5d468542c56dd951cd375aa0d92e0e8d62b9a7')
sha256sums_arm=('6dfae03e0405afc8da65935882ed60998bdb759445aa52895693ce10cf5d9d06')

package() {
    # Upstream uses different format for architecture notation
    case "${CARCH}" in
        'x86_64')   _subarch='amd64' ;;
        'aarch64')  _subarch='arm64' ;;
        'i686')     _subarch='386'   ;;
        *)          _subarch="${CARCH}"  ;;
    esac

    # Install license and binary
    install -Dm644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm755 "${srcdir}/${_shortname}" "${pkgdir}/usr/bin/${_shortname}"
}
