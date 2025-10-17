# Maintainer:   fft <nobody@nowhere.no>
# Contributor:  oech3
# Contributor:  Daniele Basso <daniele05 dot bass at gmail dot com>
# Contributor:  Dimitris Kiziridis <ragouel at outlook dot com>

pkgname=codelobster
pkgver=2.6.0
pkgrel=3
pkgdesc='Free cross-platform IDE for PHP/HTML/CSS/JavaScript development'
arch=('x86_64')
url="https://www.codelobsteride.com"
license=("custom:${pkgname}")
provides=('codelobster-ide')
makedepends=(patchelf)
depends=(
    curl hicolor-icon-theme libssh libxcb rtmpdump quazip-qt5
    qt5-{base,declarative,imageformats,svg,webengine,websockets,xmlpatterns}
)

optdepends=(libmysqlclient57 qt5-{virtualkeyboard,wayland,webglplugin})

source=(
    "https://codelobsteride.com/download/codelobsteride-${pkgver}_amd64.deb"
    'LICENSE'
)

sha256sums=(
    '56ad35fe9ee5cd26bbd49b14331365afc670a93da3079e560bd5e3d2cb5b4366'
    '70ce1193a0036cff727f29e1c94bd3ddd61599993ba5d130491037b91158a73a'
)

build() {
    tar xf data.tar.xz
    rm usr/bin/codelobster~ usr/share/applications/codelobsteride.desktop~
    ln -sf /opt/codelobsteride/CodeLobsterIDE usr/bin/codelobster

    cd opt/codelobsteride
    rm libasn1.so.8 libcrypto.so.1.1 libcurl.so.4 libhogweed.so.4 libicudata.so* libicui18n.so* libicuuc.so* libidn.so.11 liblber-2.4.so.2 \
       libldap_r-2.4.so.2 libmysqlclient.so.20 libnettle.so.6 librtmp.so.1 libssl.so.1.1 libquazip.so.1 libxcb-* libQt5* qt.conf QtWebEngineProcess
    rm -r iconengines imageformats platforminputcontexts platforms printsupport sqldrivers translations xcbglintegrations
    rm -r resources # NB: we delete here icudtl.dat, but there is no corresponding file in /usr.
    find ./ -name "*.so*" -exec chmod -x {} +

# next C++ functions/operators compiled with @Qt_5 version:
#  $ c++filt _ZdaPvm _ZdlPvm __cxa_throw_bad_array_new_length _ZSt24__throw_out_of_range_fmtPKcz _ZNSt13runtime_errorC2ERKS_ _ZNSt13runtime_errorC2EPKc
#      operator delete[](void*, unsigned long)
#      operator delete(void*, unsigned long)
#      __cxa_throw_bad_array_new_length
#      std::__throw_out_of_range_fmt(char const*, ...)
#      std::runtime_error::runtime_error(std::runtime_error const&)
#      std::runtime_error::runtime_error(char const*)
# Delete this version to make CodelobsterIDE workable. Approach was proposed by oech3.
    for sym in __ZdaPvm _ZdlPvm __cxa_throw_bad_array_new_length _ZSt24__throw_out_of_range_fmtPKcz _ZNSt13runtime_errorC2ERKS_ _ZNSt13runtime_errorC2EPKc; do
        for file in CodeLobsterIDE lib*.so.1 ./Plugins/lib*.so; do
            patchelf $file --clear-symbol-version $sym
        done
    done

    ln -sf /usr/lib/libquazip1-qt5.so libquazip.so.1
}

package() {
    mv usr opt "${pkgdir}"
    install -Dm644 "${srcdir}/LICENSE" -t "${pkgdir}/usr/share/licenses/${pkgname}/"
}
