# Maintainer: Winston Astrachan <winston dot astrachan at gmail dot com>

pkgname=google-cloud-cli-gke-gcloud-auth-plugin
pkgver=542.0.0
pkgrel=1
pkgdesc="A google-cloud-cli component that provides a kubectl authentication plugin for GKE."
arch=('x86_64' 'aarch64')
url="https://cloud.google.com/blog/products/containers-kubernetes/kubectl-auth-changes-in-gke"
license=('Apache-2.0')
depends=('google-cloud-cli' 'kubectl>=1.26')
options=('!strip')
_download_url="https://dl.google.com/dl/cloudsdk/release/downloads/for_packagers/linux"
source_x86_64=("${pkgname}-${pkgver}.orig_x86_64.tar.gz::${_download_url}/${pkgname}_${pkgver}.orig_amd64.tar.gz")
source_aarch64=("${pkgname}-${pkgver}.orig_aarch64.tar.gz::${_download_url}/${pkgname}_${pkgver}.orig_aarch64.tar.gz")
sha256sums_x86_64=('b8fb245a2f2112c3f7f45f9482cba82936e26a52d6376683e8ea9b27f053958d')
sha256sums_aarch64=('90b31175535cd05fe4ed911cbe54f1bcce5b21b9ed547c2d91f33dfbc3efbd90')

package() {
    cd "${srcdir}/google-cloud-sdk"

    # Installation paths
    _installdir="${pkgdir}/opt/google-cloud-cli"
    _bindir="${_installdir}/bin"
    _manifestdir="${_installdir}/.install"

    # Architecture mapping
    case "${CARCH}" in
        'aarch64') _subarch='arm' ;;
        *)         _subarch="${CARCH}" ;;
    esac

    # Create installation directories
    install -dm755 "${_manifestdir}"
    install -dm755 "${_bindir}"
    install -dm755 "${pkgdir}/usr/bin"

    # Install plugin manifests and snapshots
    _manifests=(
        "gke-gcloud-auth-plugin-linux-${_subarch}.manifest"
        "gke-gcloud-auth-plugin-linux-${_subarch}.snapshot.json"
        "gke-gcloud-auth-plugin.manifest"
        "gke-gcloud-auth-plugin.snapshot.json"
    )

    for _item in "${_manifests[@]}"; do
        install -Dm644 ".install/${_item}" "${_manifestdir}/${_item}"
    done

    # Install plugin binary
    install -Dm755 "bin/gke-gcloud-auth-plugin" "${_bindir}/gke-gcloud-auth-plugin"

    # Symlink plugin binary to standard path
    ln -sf "/opt/google-cloud-cli/bin/gke-gcloud-auth-plugin" "${pkgdir}/usr/bin/gke-gcloud-auth-plugin"
}
