# Maintainer: imcb <irismessage@protonmail.com>

pkgname='gp2-git'
pkgver=r1077.b34765e
pkgrel=1
pkgdesc="The rule-based graph programming language GP 2"
arch=('x86_64')
url="https://uoycs-plasma.github.io/GP2/"
license=('GPL-3.0-only')
depends=(
    'bash'
    'glibc'
    'glib2'
    # these are needed at runtime because of how it works
    'judy'
    'autoconf'
    'automake'
    'binutils'
    'bison'
    'flex'
    'gcc'
    'make'
)
makedepends=(
    'git'
    # patch fixes this
    # 'pandoc'
)
checkdepends=()
optdepends=()
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=(
    "${pkgname}::git+https://github.com/UoYCS-plasma/GP2.git"
    'https://gist.githubusercontent.com/ismaili-ziad/0e2b06cb0f1a896ac99b2f2a481d39c5/raw/8adad53661c49ce817ee1f63d9056b72917ec755/gp2c'
    "${pkgname}.patch"
)
sha256sums=('SKIP'
            '3047cb18c916bb503b2dc6f0f312a8f66c713b2a749ac1668856b6b562c1bdc0'
            'e1541c0e62243cf630b44c0baec81df94532271a6568c04cde14b365b0b4fd45')

pkgver() {
    cd "${pkgname}"

    # If there are no tags then use number of revisions since beginning of the history:
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

prepare() {
    cd "${pkgname}"

    cp --dereference "${srcdir}/gp2c" "bin/gp2c"
    patch -p1 -i "${srcdir}/${pkgname}.patch"
}

build() {
    cd "${pkgname}"

    # software has buffer overflow problem with 3 (the arch default)
    export CFLAGS="${CFLAGS/D_FORTIFY_SOURCE=3/D_FORTIFY_SOURCE=2}"

    autoreconf -i
    ./configure --prefix=/opt/gp2
    make
}

# check() {
#     cd "${pkgname}"
#
#     make -k check
# }

package() {
    cd "${pkgname}"

    make DESTDIR="${pkgdir}/" install

    # this system heavily needs improving upstream
    cp -r "lib/"* "${pkgdir}/opt/gp2/lib/"

    # install gp2c
    install -Dm755 "bin/gp2c" "${pkgdir}/opt/gp2/bin/gp2c"

    # link binaries
    install -d "${pkgdir}/usr/bin"
    ln -s "/opt/gp2/bin/gp2" "${pkgdir}/usr/bin/gp2"
    ln -s "/opt/gp2/bin/gp2c" "${pkgdir}/usr/bin/gp2c"
}
