# Maintainer: Jakub Kopańko <hi at kopanko dot com>

pkgname=hcp-bin
pkgver=0.10.0
pkgrel=1
pkgdesc="Lets you administer HashiCorp Cloud Platform (HCP) resources and services."
arch=('x86_64' 'aarch64')
url="https://github.com/hashicorp/hcp"
license=("MPL-2.0")
provides=("hcp=${pkgver}")
conflicts=('hcp')

source_x86_64=("https://releases.hashicorp.com/hcp/${pkgver}/hcp_${pkgver}_linux_amd64.zip")
sha256sums_x86_64=('d9f0af27a87c4bf43ab15139985c99a4c70b0e3e37b64d1a97e6978550fb79fe')

source_aarch64=("https://releases.hashicorp.com/hcp/${pkgver}/hcp_${pkgver}_linux_arm64.zip")
sha256sums_aarch64=('3c9becec5ce1feb9481600bc2b39c71fbed025c3183382478edcaf8dc11425c9')

package() {
    install -Dm755 "${srcdir}/hcp" "${pkgdir}/usr/bin/hcp"
}
