# Maintainer: Aru Sahni <aru@arusahni.net>
pkgname=dbus-executor
pkgver=0.1.0
pkgrel=2
epoch=
pkgdesc="Launch arbitrary programs via D-Bus."
arch=('x86_64')
url="https://github.com/arusahni/dbus-executor/"
license=('MPL-2.0')
groups=()
depends=()
makedepends=('cargo' 'sed')
checkdepends=()
optdepends=()
provides=('dbus-executor')
conflicts=('dbus-executor')
replaces=()
backup=()
options=()
install=
changelog=
source=("$pkgname-$pkgver.tar.gz::https://github.com/arusahni/$pkgname/archive/v$pkgver.tar.gz")
noextract=()
sha256sums=('852fb3d34291da3fe7a6d9404ed351da9491d6c0add676395454c397af0e3002')
validpgpkeys=()

build() {
    cd "$pkgname-$pkgver"
    cargo build --release --locked
}

check() {
    true
}

package() {
    cd "$pkgname-$pkgver"
    cargo install --root "${pkgdir}"/usr --path "${srcdir}/${pkgname}-${pkgver}"
    # Random metadata file created by cargo. See https://github.com/rust-lang/cargo/issues/6797
    rm "${pkgdir}"/usr/.crates.toml "${pkgdir}"/usr/.crates2.json
    sed -i 's|^Exec=.*|Exec=/usr/bin/dbus-executor|' "${srcdir}/${pkgname}-${pkgver}/net.arusahni.dbusexecutor.service"
    install -D -m644 "${srcdir}/${pkgname}-${pkgver}/net.arusahni.dbusexecutor.service" "${pkgdir}/usr/share/dbus-1/services/net.arusahni.dbusexecutor.service"
}
