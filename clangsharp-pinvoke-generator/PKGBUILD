# Maintainer: Robin 'Ruadeil' Degen <mail at ruadeil.lgbt>
pkgname=clangsharp-pinvoke-generator
pkgver=20.1.2.1
pkgrel=1
pkgdesc="A tool that takes a C/C++ header files as input and generates C# interop code"
arch=('x86_64')
url="https://github.com/dotnet/ClangSharp"
options=(!strip)
license=('MIT')
depends=(
  'dotnet-runtime-8.0'
  'llvm'
  'llvm-libs'
  'clang'
)
makedepends=('dotnet-sdk-8.0' 'cmake')
source=(
    "${pkgname}-${pkgver}.tar.gz::https://github.com/dotnet/ClangSharp/archive/refs/tags/v${pkgver}.tar.gz"
    "001-cmake-version-fix.patch"
    "002-arch-clang-cpp-libs.patch"
)
sha256sums=('9abc502a4d53e82b57606d6f89e027ed61e8e1aa637e3b95b1840340913c2a3c'
            'cb402c2415a4a0fbe8dc89d33f2febbfd6a0f0be67e4e40608dda37d8f64af20'
            '3b2d6e5ad0b8581247de3139702067e7c7a4e76ad2c6316a50101fce5d0e1ecf')
_libver=20.1.2

prepare() {
    cd ClangSharp-${pkgver}

    # Fix CMake 4.0 compatibility issue
    patch -Np1 -i "../001-cmake-version-fix.patch"

    # Arch packs all clang libraries as libclang-cpp.so
    patch -Np1 -i "../002-arch-clang-cpp-libs.patch"
}

build() {
    local cmake_options=(
        -B cmake_build
        -S ClangSharp-${pkgver}
        -DCMAKE_BUILD_TYPE=Release
    )

    cmake "${cmake_options[@]}"
    cmake --build cmake_build
    dotnet publish \
        ClangSharp-${pkgver}/sources/ClangSharpPInvokeGenerator/ClangSharpPInvokeGenerator.csproj \
        --runtime linux-x64 \
        --sc \
        -o "${srcdir}/build" \
        -c Release \
        -f net8.0 \
        -p:AnalysisLevel=None \
        -p:DebugType=None \
        -p:DebugSymbols=false \
        -p:PublishTrimmed=false \
        -p:PublishReadyToRun=true \
        -p:PublishSingleFile=true \
        -p:IncludeNativeLibrariesForSelfExtract=true \
        -p:PackAsTool=false
}

check() {
    dotnet test ./ClangSharp-${pkgver}/ClangSharp.sln -c Release -f net8.0 --no-build
}

package() {
    install -Dm755 "${srcdir}/build/ClangSharpPInvokeGenerator" "${pkgdir}/usr/bin/ClangSharpPInvokeGenerator"
    ln -s "ClangSharpPInvokeGenerator" "${pkgdir}/usr/bin/clangsharp-pinvoke-generator"
    install -Dm644 "${srcdir}/ClangSharp-${pkgver}/LICENSE.md" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.md"
    install -Dm644 "${srcdir}/cmake_build/lib/libClangSharp.so.${_libver}" "${pkgdir}/usr/lib/libClangSharp.so.${_libver}"
    ln -s "libClangSharp.so.${_libver}" "${pkgdir}/usr/lib/libClangSharp.so"
}
