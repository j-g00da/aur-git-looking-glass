# Maintainer: Sander Kolman <Sandarr95@users.noreply.github.com>
pkgname=decky-loader-bin
pkgver=3.1.3
pkgrel=1
pkgdesc="Unofficial Arch build of Decky Loader, a homebrew plugin launcher for the Steam Deck."
arch=('x86_64')
url="https://github.com/SteamDeckHomebrew/decky-loader"
license=('MIT')
provides=('decky-loader')
conflicts=('decky-loader')
source=("PluginLoader::${url}/releases/download/v${pkgver}/PluginLoader"
        "decky-loader@.service::${url}/raw/v${pkgver}/dist/plugin_loader-release.service"
        "decky-loader-helper")
sha256sums=('cb035a3f1f4181ff2e9823cba202d7e1a260b4f68cec06fd25acc7850f101cfe'
            '64d6aa626aa45e1659e3137aa3afd72edd840094199d62bb6ff2e73c5ce738b1'
            'SKIP')

build() {
    sed -i "s|\${HOMEBREW_FOLDER}|/home/%i/.local/var/opt/decky-loader|" "${srcdir}/decky-loader@.service"
    sed -i "/^ExecStart=/i ExecStartPre=/usr/bin/decky-loader-helper v${pkgver} %i" "${srcdir}/decky-loader@.service"
}

package() {
    install -Dm 644 "${srcdir}/decky-loader@.service" "${pkgdir}/usr/lib/systemd/system/decky-loader@.service"
    install -Dm 644 "${srcdir}/PluginLoader" "${pkgdir}/usr/lib/decky-loader/PluginLoader"
    install -Dm 755 "${srcdir}/decky-loader-helper" "${pkgdir}/usr/bin/decky-loader-helper"
}
