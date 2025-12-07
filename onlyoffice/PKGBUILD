# Maintainer: Levi Zim (kxxt) <rsworktech@outlook.com>
# Contributor: Daniel Bermond <dbermond@archlinux.org>
# Contributor: Mikalai Ramanovich < narod.ru: nikolay.romanovich >
pkgname=onlyoffice
pkgver=9.2.0
pkgrel=1
pkgdesc="An office suite that combines text, spreadsheet and presentation editors allowing to create, view and edit local documents"
arch=(x86_64)
url="https://www.onlyoffice.com/desktop.aspx"
license=('AGPL-3.0-only')
depends=(
    'curl' 'gtk3' 'alsa-lib' 'libpulse' 'gstreamer' 'gst-plugins-base-libs'
    'gst-plugins-ugly' 'libxss' 'nss' 'nspr' 'ttf-dejavu' 'ttf-liberation'
    'ttf-carlito' 'desktop-file-utils' 'hicolor-icon-theme'    
    'qt5-base' 'qt5-multimedia' 'qt5-x11extras' 'qt5-svg' 'libnotify'
    # System libraries introduced via patch
    'libheif' 
)
makedepends=(
    git python
    dos2unix
    nasm
    # build_tools/tools/linux/deps.py
    nodejs-lts-iron
    npm
    yarn
    grunt-cli
    cmake
    p7zip
    # v8
    ninja
    # grunt
    jdk11-openjdk
    libxml2-legacy # V8 toolchain
)
optdepends=('libreoffice: for OpenSymbol fonts'
            'otf-takao: for japanese Takao fonts'
            'ttf-ms-fonts: for Microsoft fonts'
            'gst-plugins-good: for playing embedded video files'
            'gst-libav: for playing embedded video files')
conflicts=(onlyoffice-bin onlyoffice-git)
options=(
    '!emptydirs'
    '!lto'
)
_url=https://github.com/ONLYOFFICE
# The tag used for sumodules
_tag=v9.2.0.102
# ICU: scripts/core_common/modules/icu.py
_icu_major=74
_icu_minor=2
source=(
    # Source
    "git+${_url}/DesktopEditors#tag=v$pkgver"
    "$pkgname-core::git+${_url}/core#tag=$_tag"
    "$pkgname-desktop-apps::git+${_url}/desktop-apps#tag=$_tag"
    "$pkgname-desktop-sdk::git+${_url}/desktop-sdk#tag=$_tag"
    "$pkgname-dictionaries::git+${_url}/dictionaries#tag=$_tag"
    "$pkgname-sdkjs::git+${_url}/sdkjs#tag=$_tag"
    "$pkgname-sdkjs-forms::git+${_url}/sdkjs-forms#tag=$_tag"
    "$pkgname-web-apps::git+${_url}/web-apps#tag=$_tag"
    "$pkgname-build_tools::git+${_url}/build_tools#tag=$_tag"
    "$pkgname-core-fonts::git+${_url}/core-fonts#tag=$_tag"
    "$pkgname-document-templates::git+${_url}/document-templates#tag=$_tag"
    "onlyoffice.github.io::git+${_url}/onlyoffice.github.io"
    # V8
    "git+https://chromium.googlesource.com/chromium/tools/depot_tools.git#commit=8dde9800ee2b8326ab11a87abd67d3bd9f8c8773"
    "git+https://github.com/v8/v8#tag=9.0.257.43" # 9.0-lkgr
    # ICU -- Keep in Sync with build_tools/scripts/core_common/modules/icu.py 
    "git+https://github.com/unicode-org/icu.git#tag=release-$_icu_major-$_icu_minor"
    # Patches
    "v8-89-fix-cstdint.diff"
    "0001-Add-update-only-to-avoid-download-and-build-at-once.patch"
    "0002-Add-no-third-party-update-and-update-third-party-onl.patch"
    "0003-use-QT_VERSION-env-instead-of-guessing.patch"
    "0004-Only-build-tar.patch"
    "0001-Fix-boost-module-import.patch"
    "0001-Disable-static-linking-of-libstdc.patch"
    "0001-Dynamically-link-libstdc-in-icu.patch"
    "use-fpermissive.diff"
    "fix-glib-qt-macro-collision.diff"
    fix-limits-include{,-1}.diff
    "do-not-build-commercial.diff"
    system-heif{,-0}.diff
    "fix-QDesktopWidget-include.diff"
)
sha256sums=('44e133e174426fbf7b998e379edc73740cb5ea55a370518181f14cbfb9996ba3'
            'a0f51ae6ebe0bdbc0eb561ad4b1fc238172ba69c71a59628573cdf29564e8ef5'
            '100d1b25f316272539376754c1393faf70928074a6e83d5e44cc0c7589d670e0'
            '1de7e1b133ca497f914a48bde13d04f54da220d7954076d6b1006c7898058b2e'
            '62dc945a78f38ab87e9d0a1a0cfefe0ddee29ba9de4e48468f7047d0aac4e645'
            '654d33d3163d95b33eb20cb1ea8afe0002faeccf7387e6e5689ecb99f4ea0ebe'
            '486b5d37ecbbd68d0b3724724ee0bb2146b39cadd8a5e72d498ef8ddf733ba16'
            'ee186d380736673fda48a14e48c6d3e51185dc9729b8ae555ad6193533b7577c'
            '444c596bef0fffdb102ce3dee819a8f99ce3817bd4405adfbcd63082a4f3024b'
            '55c1d70a8bdd8f818af8e4c784bfc03f0569fcb863cc6797f888b749153ed720'
            '1a9ddf334ee246bcd4f412475f91dd2a70408521998f358dbcae18976f861e56'
            'SKIP'
            'cd7a982bf79eae86a8b7727193e2a9feccd1388cd0cc474b8d786ac6dc695cfe'
            '8cd5a305b9ce85066094963a5d28ad221f9598b9e98e569bf47c61f570c2988b'
            '1370503ff352608f587486324bde040a9038f4cbf2d21085f821121dd49dbede'
            '9f570942c7467c800acb4b891f7739a1fcd497dbb2d30b04005e0b6a38da6e4d'
            'a4f2502acfdc48d3daad5ed166c1cd15cb0595a4d5018f22d9390f73f25dd8c6'
            'e9d56d030039ad72e89dc48877f7fccaeac4cfa5ff584833849be2601fca5fb7'
            'bdcf095fd46fb47f2992510078c46cef2b0084000ff4a0c4f956efb0db7e4d57'
            '0f7acc17b78eaeb338f098088ee11356045a53af6698c79ada45fa261c8d18fe'
            '95e107a7c2a895866e8a1d4c89bb4dbed50027fff9e5b9ab513c556537554eef'
            'b3e040f0551dc469d91d23487e05bdb7123d2a3e50c5180c44be868a6f42ecbf'
            'a3561d1f18a61c404c8f9f9ed51484b2e19e3caaee86b71b1cabe3c7ccd0053a'
            '222dab12468f27b2bc1cc098ad2e4ca5bff8df845939f5cba2efff2165eafbcd'
            '2c698dc512b4b0d94c8e427a2ac9a6f3e92aeb1c33414c30dfc48fa44832f6ec'
            'cb87384ce721ac15a82d254efe8662be0eb9011c122edfcb1caa07194fbae697'
            '8761a41683733f8c297fda55485126e895b1271aefd0f834078eb417878afbb0'
            'b7bce5799d2f52026795169e40d6a3b436bb8c481d769cc8ff9df19a7e9e29cd'
            'c328fbadbb34f6fd59b79b2be188877ae2652a932d1b003548632c261f88a9c6'
            'e3af225ba3945e1430d4dbc2a4049e3ff3e114f5e73616624e430eed813b744f'
            '7849b1895a7b99479b2a78a8f009a3e670b0588a5bad150168506a4e41d03e69')


_set_flags() {
    # Set CXX standard to gnu++11. It appears that upstream forgot to do so in
    # some places.
    if [[ ! "$CXXFLAGS" =~ '-std=' ]]; then
        CXXFLAGS="$CXXFLAGS -std=gnu++11"
    fi
    # Some dependencies are still using legacy cmake versions
    export CMAKE_POLICY_VERSION_MINIMUM=3.5
}

prepare() {
    _set_flags
    for _module in core desktop-{apps,sdk} dictionaries sdkjs{,-forms} \
        web-apps build_tools document-templates core-fonts
    do
        mv "$pkgname-${_module}" "${_module}"
    done
    cp -r icu/icu4c core/Common/3dParty/icu/icu
    cd "$srcdir/build_tools"/tools/linux

    # Pretend that we have all dependencies installed
    touch packages_complete

    # Use system qt
    # ref: build_tools/tools/linux/use_system_qt.py
    mkdir -p system_qt/gcc_64
    ln -s /usr/bin            ./system_qt/gcc_64/bin
    ln -s /usr/lib            ./system_qt/gcc_64/lib
    ln -s /usr/lib/qt/plugins ./system_qt/gcc_64/plugins

    # Check build_tools/tools/linux/automate.py for options to configure.py
    cd "$srcdir/build_tools"
    patch -Np1 -i ../0001-Fix-boost-module-import.patch
    patch -Np1 -i ../0001-Add-update-only-to-avoid-download-and-build-at-once.patch
    patch -Np1 -i ../0002-Add-no-third-party-update-and-update-third-party-onl.patch
    # Fix the way to get qt version
    patch -Np1 -i ../0003-use-QT_VERSION-env-instead-of-guessing.patch
    # Don't build debs/rpm/..
    patch -Np1 -i ../0004-Only-build-tar.patch
    # Dyn linking system libs for vendored ICU
    patch -Np1 -i ../0001-Dynamically-link-libstdc-in-icu.patch
    # Do not build commerical edition
    patch -Np0 -i ../do-not-build-commercial.diff
    # Use https when download CEF
    sed -i 's|http://|https://|' ./scripts/core_common/modules/cef.py

    # We manually update the sources, so --update 0
    ./configure.py --module desktop --update 0 --branch "tags/$_tag" --qt-dir "$(realpath tools/linux/system_qt)"
    ./make.py --update-only

    # fetch V8 before updating third party to have a chance to patch it
    cd "$srcdir/"
    mv depot_tools core/Common/3dParty/v8_89/
    cd core/Common/3dParty/v8_89/
    cat >.gclient <<EOF
solutions = [
  {
    "name": "v8",
    "url": "file://${srcdir}/v8@makepkg",
    "deps_file": "DEPS",
    "managed": False,
    "custom_deps": {},
    "custom_vars": {},
  },
]
EOF
    export PATH="$(pwd)/depot_tools:$PATH" DEPOT_TOOLS_UPDATE=0
    # ref: build_tools/scripts/core_common/modules/v8_89.py
    gclient sync --force
    # V8 use system libstdc++
    ln -sf /usr/lib/libstdc++.so.6 \
        v8/third_party/llvm-build/Release+Asserts/lib/libstdc++.so.6
    patch -Np1 -d v8 < "$srcdir/v8-89-fix-cstdint.diff"

    # We need to apply the patches after the update
    cd "$srcdir"
    patch -Np0 -i system-heif.diff
    patch -Np0 -i fix-limits-include-1.diff
    patch -Np0 -i fix-QDesktopWidget-include.diff
    patch -Np0 -i system-heif-0.diff
    patch -Np1 -d core < 0001-Disable-static-linking-of-libstdc.patch
    # Fix some compile error
    patch -Np1 -d core < use-fpermissive.diff
    dos2unix core/Common/OfficeFileFormatChecker2.cpp
    patch -Np0 -d core < fix-limits-include.diff
    patch -Np0 -d desktop-apps < fix-glib-qt-macro-collision.diff
    # patch -Np1 -d desktop-apps < package-add-dir-target.diff
    # pragma (end)?region breaks if-else-if. Is this a gcc bug?
    sed -Ei '/pragma (end)?region/d' core/MsBinaryFile/XlsFile/Format/Logic/Biff_structures/StringPtgParser.cpp 
    # Fix missing unistd.h
    # TODO: use system zlib
    sed -i '1s/^/#include<unistd.h>\n/' core/OfficeUtils/src/zlib-1.2.11/gzwrite.c
    sed -i '1s/^/#include<unistd.h>\n/' core/OfficeUtils/src/zlib-1.2.11/gzread.c
    sed -i '1s/^/#include<unistd.h>\n/' core/OfficeUtils/src/zlib-1.2.11/gzlib.c
    sed -i '1s/^/#include<cmath>\n/' desktop-sdk/ChromiumBasedEditors/videoplayerlib/src/qtimelabel.cpp
    sed -i '1s/^/#include<cmath>\n/' desktop-sdk/ChromiumBasedEditors/videoplayerlib/src/qvideoslider.cpp
    sed -i '1s/^/#include<cmath>\n/' desktop-sdk/ChromiumBasedEditors/videoplayerlib/src/qvideoplaylist.cpp
    sed -i '1s/^/#include<QPainterPath>\n/' desktop-apps/win-linux/src/windows/platform_linux/cwindowplatform.cpp

    cd "$srcdir/build_tools"
    ./make.py --update-third-party-only
}

build() {
    _set_flags
    cd build_tools
    local qt_ver="$(pacman -Q qt5-base | awk '{print $2}')"
    export QT_VERSION="${qt_ver//+*}"

    export CFLAGS="${CFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"
    export CXXFLAGS="${CXXFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"
    # -O2 causes a linker segfault during LTO
    export CFLAGS="${CFLAGS/-O2/}"
    export CXXFLAGS="${CXXFLAGS/-O2/}"
    # GLIBCXX_ASSERTIONS causes undefined symbols during linking
    export CXXFLAGS="${CXXFLAGS/-Wp,-D_GLIBCXX_ASSERTIONS/}"

    ./make.py --no-third-party-update
}

package() {
    cd build_tools
    ./make_package.py -P linux_x86_64 -T desktop -V "$pkgver" -B "$pkgrel"
    cd ../desktop-apps/win-linux/package/linux/tar
    tar xf onlyoffice-desktopeditors-"$pkgver"-"$pkgrel"-"$CARCH".tar.xz
    rm -f *.tar.xz

    install -d "$pkgdir"/opt/onlyoffice
    cp -r usr "$pkgdir"
    chmod +x "$pkgdir"/usr/bin/*
    # Symlink for backward compatibility
    ln -s onlyoffice-desktopeditors "$pkgdir"/usr/bin/desktopeditors
    cp -r opt "$pkgdir"

    # We are using system Qt5 and icu
    rm "$pkgdir"/opt/onlyoffice/desktopeditors/libQt5*
    rm "$pkgdir"/opt/onlyoffice/desktopeditors/libicu*
}
