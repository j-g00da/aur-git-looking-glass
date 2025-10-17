# Maintainer: Sander Kolman <Sandarr95@users.noreply.github.com>
pkgname='decky-loader-prerelease-bin'
_pkgver=3.1.3-pre2
pkgver="${_pkgver//-/_}"
pkgrel=1
pkgdesc="Unofficial Arch build of Decky Loader (pre-release), a homebrew plugin launcher for the Steam Deck."
arch=('x86_64')
url="https://github.com/SteamDeckHomebrew/decky-loader"
license=('MIT')
provides=('decky-loader')
conflicts=('decky-loader')
source=("PluginLoader::${url}/releases/download/v${_pkgver}/PluginLoader"
        "decky-loader@.service::${url}/raw/v${_pkgver}/dist/plugin_loader-release.service"
        "decky-loader-helper")
sha256sums=('46b6aa1c63cc86b49eb5a8d576e68c876f224e66f09d3ff2ad027a609b95c16d'
            '64d6aa626aa45e1659e3137aa3afd72edd840094199d62bb6ff2e73c5ce738b1'
            'SKIP')

build() {
    sed -i "s|\${HOMEBREW_FOLDER}|/home/%i/.local/var/opt/decky-loader|" "${srcdir}/decky-loader@.service"
    sed -i "/^ExecStart=/i ExecStartPre=/usr/bin/decky-loader-helper v${_pkgver} %i" "${srcdir}/decky-loader@.service"
}

package() {
    install -Dm 644 "${srcdir}/decky-loader@.service" "${pkgdir}/usr/lib/systemd/system/decky-loader@.service"
    install -Dm 644 "${srcdir}/PluginLoader" "${pkgdir}/usr/lib/decky-loader/PluginLoader"
    install -Dm 755 "${srcdir}/decky-loader-helper" "${pkgdir}/usr/bin/decky-loader-helper"
}
