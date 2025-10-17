# Contributor: Lex Black <autumn-wind@web.de>

pkgname=opencloud-web
pkgver=4.1.0
pkgrel=1
pkgdesc="Web UI for OpenCloud"
url="https://github.com/opencloud-eu/web"
arch=('aarch64' 'x86_64')
license=('AGPL-3.0-only')
makedepends=('git' 'pnpm')
install="opencloud-web.install"
backup=("var/lib/opencloud-web/config.json")
source=("${pkgname}::git+https://github.com/opencloud-eu/web.git#tag=v${pkgver/_/-}"
        "config.json")
sha512sums=('589b06f2ce662caaaa4266bf0b5cb8fb429c2391b44b7903eb8f5dcd6a179ff9bb281613d63c6a9c226986f38faa72ee15811097eea368820959b750f06af7cf'
            'c3692ff7d3f42af2c42d97d633cd14094c3b6421099b7eb74372ba9959ceca95f69c38da679b908802b7b5a5c2199484bb42ddc028e9e1372fb040fe51683e27')


build() {
    make -C ${pkgname} -j1 -f Makefile.release build
}

package() {
    # Base install location
    install -vdm755 "${pkgdir}/var/lib/${pkgname}"

    # Copy the created files from dist directory
    cp -rv ${pkgname}/dist/* "${pkgdir}/var/lib/${pkgname}"

    # Install custom web-ui config
    install -vm644 "${srcdir}/config.json" "${pkgdir}/var/lib/${pkgname}"
}
