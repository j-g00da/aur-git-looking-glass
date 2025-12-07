# Maintainer: darkhz <kmachanwenw at gmail dot com>
pkgname=bluetuith-bin
_pkgname=bluetuith
pkgver=0.2.6
pkgrel=3
pkgdesc="A TUI based bluetooth manager"
arch=('x86_64' 'i686' 'arm' 'aarch64' 'armv6h' 'armv7h')
url="https://github.com/darkhz/bluetuith"
license=('MIT')
depends=('bluez' 'bluez-obex' 'dbus')
optdepends=('networkmanager: For PANU networking'
            'modemmanager: For DUN networking'
	    'pulseaudio: For switching device audio profiles')
provides=('bluetuith')
conflicts=('bluetuith')

source_x86_64=("https://github.com/darkhz/${_pkgname}/releases/download/v${pkgver}/${_pkgname}_${pkgver}_Linux_x86_64.tar.gz")
source_arm=("https://github.com/darkhz/${_pkgname}/releases/download/v${pkgver}/${_pkgname}_${pkgver}_Linux_armv5.tar.gz")
source_aarch64=("https://github.com/darkhz/${_pkgname}/releases/download/v${pkgver}/${_pkgname}_${pkgver}_Linux_arm64.tar.gz")
source_armv6h=("https://github.com/darkhz/${_pkgname}/releases/download/v${pkgver}/${_pkgname}_${pkgver}_Linux_armv6.tar.gz")
source_armv7h=("https://github.com/darkhz/${_pkgname}/releases/download/v${pkgver}/${_pkgname}_${pkgver}_Linux_armv7.tar.gz")

sha256sums_aarch64=("63af4aae960c1754f8931c9022d926a29e9da6f82269c181d1726aad61312d92")
sha256sums_arm=("dc48b9e1edbae8358db940ad5972e902a509996fbd66c9d4619adab5b3e4a681")
sha256sums_armv6h=("317b3ddffd4f368b5bdf0bf6f5e80995d7a77b985415d2b8bc35444b6314e0d4")
sha256sums_armv7h=("f443c29f465b2dc655becbc1e258c2525ad080bb2b390c2e2cf5b3e407df6629")
sha256sums_i686=("5feece622f7af5e86dcb4d6207f7b33499af9c7408d223fe59defc73af2d98f8")
sha256sums_x86_64=("f206731d16c446ade39907dc88f961ed3ef07a12911cf7432a2b768aefa62717")

package() {
  install -Dm 755 "${_pkgname}" -t "${pkgdir}/usr/bin"
}
