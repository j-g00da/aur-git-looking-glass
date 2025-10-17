# Maintainer: o.s.dv.f@seznam.cz
pkgname=deshader-git
pkgver=rb5aee41
pkgrel=1
pkgdesc="Shader debugging via GLSL code instrumentation. This is preliminary package, does not coply with all package guidelines."
arch=(armv7h
      aarch64
      x86_64
      i686)
url="https://github.com/OSDVF/deshader"
depends=('gtk3'
         'webkit2gtk')
makedepends=('git'
             'zig=0.14.0'
             'binutils'
             'unzip'
             'curl'
             'zip'
             'tar'
             'pkgconf'
             )
optdepends=()
options=(!lto !strip)
provides=("deshader=$pkgver"
          "deshader-run=$pkgver"
          "libdeshader.so")
conflicts=('deshader'
          'deshader-run')
source=('deshader.desktop'
        '48.png'
        '256.png'
        'scalable.svg'
        'git+https://github.com/OSDVF/deshader.git')
sha256sums=('fba58063082fef9ea30cb88a73ac1877360abcca0cef36859a3ee096528fcd12'
            '00bcebeeb6423504e5b877c398751bfa15df23266131ffe1fb3058e2f1511de4'
            'dd20694f4cc973e44ce5df87a7da166515aa9df6a8045fa13df726980308aa92'
            '067392a62f68bf6354c9fefc34788b9a350f56e19ac899248da1142df7541e4b'
            'SKIP')
license=('GPL-3.0-or-later')

pkgver() {
    cd "$srcdir/${pkgname%-git}" || exit 1
    MAYBE_TAG=$(git describe --tags --abbrev=0 --exact-match 2>/dev/null || echo "")
    if [[ "$MAYBE_TAG" != "" ]] && [[ $MAYBE_TAG =~ ^[[:digit:]] ]]; then 
        echo $MAYBE_TAG # tag that begins with a digit => release version, use tag name
    else 
        printf "r%s" "$(git rev-parse --short HEAD)" # no tag or dev tag => development version, use commit hash
    fi
}

build_deshader() {
    zig build deshader --release=safe # do not override build flags by makepkg
}

build_launcher() {
    zig build launcher --release=safe # do not override build flags by makepkg
}

build() {
    # do not override build flags by makepkg -- will corrupt the build for use with Zig
    export CFLAGS=""
    export CXXFLAGS=""
    export CPPFLAGS=""
    if [[ "$OSTYPE" == "linux*" ]]; then
        export LDFLAGS="-z,itb,-z,shstk"
    fi

    cd "$srcdir/${pkgname%-git}" || exit 1
    if ! build_deshader; then # must be ran twice to fix the C import
        sh fix_c_import.sh
        echo "Retrying build"
        if ! build_deshader; then # maybe three times
            sh fix_c_import.sh
            echo "Retrying build third time"
            build_deshader
        fi
    fi
    if ! build_launcher; then # must be ran twice to fix the C import
        sh fix_c_import.sh
        echo "Retrying launcher build"
        if ! build_launcher; then # maybe three times
            sh fix_c_import.sh
            echo "Retrying launcher build third time"
            build_launcher
        fi
    fi
}

check() {
    pass=false
    if [[ "$OSTYPE" == darwin* ]]; then
        LIBEXT=dylib
    else
        LIBEXT=so
    fi
    output=`DESHADER_LIB="$srcdir/${pkgname%-git}/zig-out/lib/libdeshader.$LIBEXT" "$srcdir/${pkgname%-git}/zig-out/bin/deshader-run" --version`
    for line in $output
    do
        if [ "$pkgver" == "$line" ] || [ $pkgver == "r$line" ]; then
            pass=true
            echo "Built $pkgver matches"
            break
        fi
    done
    if ! $pass; then
        echo "Version $pkgver does not match $output"
        exit 1
    fi
}

prepare() {
    export PATH="$srcdir/dep/bin:$srcdir/vcpkg:$PATH"
    export ZIG_GLOBAL_CACHE_DIR="$srcdir/dep/.zig-cache"
    export VCPKG_DEFAULT_BINARY_CACHE_DIR="$srcdir/dep/.vcpkg-cache"
    export VCPKG_DISABLE_METRICS=1

    # get the submodules
    cd "$srcdir/${pkgname%-git}" || exit 1

    git submodule update --init --recursive

    cd "$srcdir" || exit 1
    # check for bun in the path
    if ! command -v bun; then
        # download bun
        curl -fsSL https://bun.sh/install | BUN_INSTALL="$srcdir/dep" bash
    fi

    # check for VCPKG
    if ! command -v vcpkg; then
        # check for downloaded VCPKG repository
        if [ -d "$srcdir/vcpkg" ]; then
            # check if it is a git repository
            if [ -d "$srcdir/vcpkg/.git" ]; then
                # update VCPKG
                cd "$srcdir/vcpkg" || exit 1
                git pull
            else
                # remove the directory
                rm -rf "$srcdir/vcpkg"
            fi
        
        else
            # download VCPKG
            git clone https://github.com/microsoft/vcpkg.git
        fi
        cd "$srcdir/vcpkg" || exit 1
        chmod +x ./bootstrap-vcpkg.sh
        ./bootstrap-vcpkg.sh
    fi
}

package() {
    install -d "${pkgdir}/usr/bin"
    install -d "${pkgdir}/usr/lib"
    install -d "${pkgdir}/usr/share/applications"
    install -d "${pkgdir}/usr/share/icons/hicolor/48x48/apps"
    install -d "${pkgdir}/usr/share/icons/hicolor/256x256/apps"
    install -d "${pkgdir}/usr/share/icons/hicolor/scalable/apps"

    install -m755 "$srcdir/${pkgname%-git}/zig-out/bin/deshader-run" "$pkgdir/usr/bin/deshader-run"
    install -m755 "$srcdir/${pkgname%-git}/zig-out/lib/libdeshader.so" "$pkgdir/usr/lib/libdeshader.so"

    #install headers
    install -d "${pkgdir}/usr/include/deshader"
    for h in "$srcdir/${pkgname%-git}/zig-out/include/deshader/"*; do
        install -m644 "$h" "$pkgdir/usr/include/deshader/"
    done

    #install desktop file and icons
    install -m644 "$srcdir/deshader.desktop" "$pkgdir/usr/share/applications/deshader.desktop"
    install -m644 "$srcdir/48.png" "$pkgdir/usr/share/icons/hicolor/48x48/apps/deshader.png"
    install -m644 "$srcdir/256.png" "$pkgdir/usr/share/icons/hicolor/256x256/apps/deshader.png"
    install -m644 "$srcdir/scalable.svg" "$pkgdir/usr/share/icons/hicolor/scalable/apps/deshader.svg"
}
