# Maintainer: Antti Ellilä <antti@antti.codes>
# Contributor: Jaime Martínez Rincón <jaime(at)jamezrin(dot)name>

pkgname=httptoolkit
pkgver=1.23.2
pkgrel=1
epoch=1
pkgdesc="Beautiful, cross-platform & open-source HTTP(S) proxy, analyzer and client."
arch=("x86_64")
url="https://httptoolkit.com/"
license=('AGPL-3.0-or-later')

# package.json specifies electron 37 as of version 1.23.0
_electron_version=37

depends=("electron${_electron_version}" python)
makedepends=(git npm)

_pkgrepo="https://github.com/httptoolkit/httptoolkit-desktop"
source=("$pkgname-$pkgver.tar.gz::${_pkgrepo}/archive/refs/tags/v${pkgver}.tar.gz"
        'httptoolkit.desktop')

sha256sums=('df89912400f6716b7ccb333240764eaaac6d8a6b240e3ac098f7b019078332b9'
            'e8a8fd3ce7983753d3c990402c079a7876aad9b08e1822b5494ce4abdfc1a544')

_archive_name="httptoolkit-desktop"
prepare() {
    cd "${srcdir}/${_archive_name}-${pkgver}"
    npm install --no-save --no-audit --no-progress --no-fund
}

build() {
    cd "${srcdir}/${_archive_name}-${pkgver}"
    npm run build:src
    npm run build:electron -- \
        -c.electronDist=/usr/lib/electron${_electron_version} \
        -c.electronVersion="$(cat /usr/lib/electron${_electron_version}/version)" \
        --linux dir
}

package() {
    install -d "${pkgdir}/usr/bin"
    install -d "${pkgdir}/opt/${pkgname}"
    install -d "${pkgdir}/usr/share/icons"
    install -d "${pkgdir}/usr/share/licenses"
    install -d "${pkgdir}/usr/share/applications"

    cp -r "${srcdir}/${_archive_name}-${pkgver}/dist/linux-unpacked/"* "${pkgdir}/opt/${pkgname}"
    cp "${srcdir}/${_archive_name}-${pkgver}/src/icons/icon.png" "${pkgdir}/opt/${pkgname}/icon.png"
    install -Dm644 "${srcdir}/${_archive_name}-${pkgver}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm644 "${srcdir}/${_archive_name}-${pkgver}/src/icons/icon.png" "${pkgdir}/usr/share/icons/${pkgname}.png"
    install -Dm644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications"
    _electron=${pkgdir}/opt/${pkgname}/${pkgname}
    echo "Deleting Electron binary ($(du -h "$_electron" | awk '{print $1}'))"
    rm -v "$_electron"
    install -m755 /dev/null "${pkgdir}/usr/bin/${pkgname}"
    cat >"${pkgdir}/usr/bin/${pkgname}" <<EOF
#!/bin/sh
exec electron${_electron_version} /opt/${pkgname}/resources/app.asar "\$@"
EOF
    find "$pkgdir" -name package.json -print0 | xargs -r -0 sed -i "s|$srcdir||g"
}
