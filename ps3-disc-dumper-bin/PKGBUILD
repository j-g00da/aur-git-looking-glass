# Maintainer: Viraaj Basi <viraajbasi@gmail.com>
pkgname=ps3-disc-dumper-bin
pkgver=4.4.0
pkgrel=1
pkgdesc="A handy utility to make decrypted PS3 disc dumps"
arch=('x86_64')
provides=('ps3-disc-dumper')
conflicts=('ps3-disc-dumper')
url="https://github.com/13xforever/ps3-disc-dumper"
license=('MIT')
depends=('glibc' 'zlib' 'gcc-libs')
options=('!strip')
source=(
	"https://github.com/13xforever/${pkgname/-bin/}/releases/download/v${pkgver}/${pkgname/-bin/}_linux_v${pkgver}.zip"
	"https://github.com/13xforever/${pkgname/-bin/}/archive/refs/tags/v${pkgver}.tar.gz"
	"ps3-disc-dumper.desktop"
)
b2sums=(
	'b953820e3cc8efa9d526faeb756fac9fc08522399657ef7a7e2ff590640f06ba17f3f84a4c92f330e6299c3f954f5538fb558c3bd8bf4b276322f6bc5e96d0a4'
	'78636ff31ba10b36744b0458d5c6abaa633dc604411cd1f0d271f13169a6b6819f1fa5c0a88a3557228b3605c81d7edd9b63d86544449624bdf712b414e413d4'
	'06b17f6705cd3e82e3d6cade872e25464346c00624fce88f1f5a3d3ebc1d163a4a5d0f73ba1fe07e0f5f372c7510f054976bd416bcb1088fb4b05487fcaba0d7'
)

package() {
    install -Dm755 "${srcdir}/${pkgname/-bin/}" "${pkgdir}/usr/bin/${pkgname/-bin/}"
    install -Dm644 "${srcdir}/${pkgname/-bin/}-${pkgver}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    install -Dm644 "ps3-disc-dumper.desktop" "${pkgdir}/usr/share/applications/ps3-disc-dumper.desktop"
}
