_pkgname=RedPanda-CPP
pkgname=${_pkgname,,}
pkgver=3.3
pkgrel=1
pkgdesc='A fast, lightweight, open source, and cross platform C/C++/GNU Assembly IDE'
arch=('i686' 'pentium4' 'x86_64' 'arm' 'armv6h' 'armv7h' 'aarch64' 'riscv64' 'loong64')
url="https://github.com/royqh1979/$_pkgname"
license=('GPL3')
depends=(qt6-base qt6-svg gcc gdb astyle)
makedepends=(qt6-tools imagemagick librsvg)
optdepends=(
    'clang: C/C++ compiler (alternative)'
)
optdepends_x86_64=(
    'mingw-w64-gcc: Windows C/C++ compiler'
    'wine: run Windows executable'
    'aarch64-linux-gnu-gcc: AArch64 C/C++ compiler'
    'qemu-user-static: run AArch64 executable'
    'qemu-user-static-binfmt: run AArch64 executable'
)
source=(
    "$_pkgname-$pkgver.tar.gz::https://github.com/royqh1979/$_pkgname/archive/refs/tags/v$pkgver.tar.gz"
    'compiler_hint.lua'
)
sha256sums=('4f49075e1cd163038ce571893583e56cacad8e33bde5d18765f270b0b57a4876'
            '6f887af50757c2ec7d57806b78119e0271c424db2119fbc62d111c2122c06b0c')

prepare() {
    cd "$srcdir/$_pkgname-$pkgver"
    sed -i '/CONFIG += ENABLE_LUA_ADDON/ { s/^#\s*// }' "RedPandaIDE/RedPandaIDE.pro"
}

build() {
    mkdir redpanda-build
    cd redpanda-build
    qmake6 \
        PREFIX='/usr' \
        LIBEXECDIR='/usr/lib' \
        "$srcdir/$_pkgname-$pkgver/Red_Panda_CPP.pro"
    make
}

package() {
    local _libexecdir="$pkgdir/usr/lib/RedPandaCPP"
    install -Dm644 "compiler_hint.lua" "$_libexecdir/compiler_hint.lua"

    cd redpanda-build
    make INSTALL_ROOT="$pkgdir" install

    for size in 16 22 24 32 36 48 64 72 96 128 192 256 512; do
        mkdir -p "$pkgdir/usr/share/icons/hicolor/${size}x${size}/apps"
        magick convert \
            -background none \
            "$pkgdir/usr/share/icons/hicolor/scalable/apps/redpandaide.svg" \
            -resize ${size}x${size} \
            "$pkgdir/usr/share/icons/hicolor/${size}x${size}/apps/redpandaide.png"
    done
}
