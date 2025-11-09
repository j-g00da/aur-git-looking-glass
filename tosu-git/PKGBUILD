# Maintainer: uwuclxdy
# Maintainer: Mikhail Babynichev <i@kotrik.ru>
# Contributor: Mikhail Babynichev <i@kotrik.ru>

pkgname=tosu-git
pkgver=r1390.9bfee4f
pkgrel=1
pkgdesc="Memory reader and PP counters provider for osu! and osu! Lazer"
arch=('x86_64')
url="https://github.com/tosuapp/tosu"
license=('LGPL3')
depends=()
makedepends=('git' 'pnpm' 'nodejs>=20' 'python')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
replaces=()
backup=()
options=('!strip')
install=notice.install
changelog=
source=("git+https://github.com/tosuapp/tosu.git"
        "tosu-bin.sh::https://aur.archlinux.org/cgit/aur.git/plain/tosu-bin.sh?h=tosu"
        "notice.install")
sha256sums=('SKIP'
            '16e77f6a192094be77ce1ecc9322e7296b57532851672d15f07bc82132cdfc21'
            'SKIP')
validpgpkeys=()

pkgver() {
    cd "${srcdir}/${pkgname%-git}"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cd "${srcdir}/${pkgname%-git}"
    export CXXFLAGS="${CXXFLAGS} -Wno-error=format-security"
    pnpm install --frozen-lockfile
    pnpm run build:linux
}

package() {
    cd "${srcdir}/${pkgname%-git}"
    install -Dm755 "packages/tosu/dist/tosu" "${pkgdir}/opt/tosu/tosu"
    install -d -m777 "${pkgdir}/opt/tosu"
    install -Dm755 "${srcdir}/tosu-bin.sh" "${pkgdir}/usr/bin/tosu"
}
