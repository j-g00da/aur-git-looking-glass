pkgname=kodo-browser-bin
_pkgname=kodo-browser
pkgver=2.3.2
pkgrel=3
pkgdesc="Kodo Browser 为七牛对象存储（Kodo）提供类似 Windows 资源管理器的功能。用户可以很方便的浏览文件，上传下载文件，支持断点续传等。 "
arch=('x86_64')
url="https://github.com/qiniu/kodo-browser"
license=('Apache-2.0')
depends=()
makedepends=('unzip')
source=(
    "https://github.com/qiniu/${_pkgname}/releases/download/v${pkgver}/${_pkgname}-linux-x64-v${pkgver}.zip"
    "${_pkgname}.sh"
    "${_pkgname}.desktop"
)
sha256sums=(
    'c0efcb569e2c49c12db16bef1327dddca69dd552d84425955419a775ff8cec7c'
    'fd7a00eb0b70d863e1f5f1b23c2c7b0ac8c5153ca3ba2f7778a523bcf10c89a0'
    'da1d7d01a5f569c28ba1eb9f830630de5ab7598c4cbcf6f8876d9fc97af928e2'
)

package() {
    mkdir -p "${pkgdir}/opt/${_pkgname}/release"

    # assets
    cp -r "${srcdir}/." "${pkgdir}/opt/${_pkgname}/release"
    install -Dm644 "${srcdir}/resources/app/renderer/static/brand/qiniu.png" "${pkgdir}/usr/share/icons/hicolor/scalable/apps/${_pkgname}.png"

    # binary wrapper 
    install -Dm755 "${_pkgname}.sh" "${pkgdir}/usr/bin/${_pkgname}"

    # desktop enrty
    install -Dm644 "${_pkgname}.desktop" -t "${pkgdir}/usr/share/applications/"
}
