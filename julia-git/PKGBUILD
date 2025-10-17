# Maintainer: Lex Black <autumn-wind at web dot de>
# Contributor: Antonio Rojas <arojas@archlinux.org>
# Contributor: Alexander F. Rødseth <xyproto@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: Lex Black <autumn-wind@web.de>
# Contributor: Michael Jakl <jakl.michael@gmail.com>
# Contributor: devmotion <nospam-archlinux.org@devmotion.de>
# Contributor: Valentin Churavy <v.churavy@gmail.com>
# With contributions from many kind people at https://aur.archlinux.org/packages/julia-git/

_pkgbase=julia
pkgbase=${_pkgbase}-git
pkgname=${_pkgbase}-git
pkgver=1.11.3.r56940.gd63adeda50d
pkgrel=1
arch=(x86_64)
pkgdesc='High-level, high-performance, dynamic programming language'
url='https://julialang.org/'
license=(MIT)
depends=(blas64-openblas
         fftw
         libblastrampoline
         libgit2
         libunwind
         libutf8proc
         lld
         llvm-julia-libs
         mbedtls2
         openlibm
         7zip
         pcre2
         suitesparse)
makedepends=(cmake
             git
             gcc-fortran
             libwhich
             llvm-julia
             patchelf
             python)
optdepends=('gnuplot: If using the Gaston Package from julia')
source=(git+https://github.com/JuliaLang/julia.git#branch=release-1.11
        c12e8515.patch
        julia-hardcoded-libs.patch
        julia-libgit2-1.8.patch
        julia-libgit2-1.9.patch
        julia-metainfo.patch
        julia-curl-1.10.patch)
backup=(etc/julia/startup.jl)
sha256sums=('SKIP'
            '2cc294b63e601d50341979fb936826bdba59de2165a5929eae927e152652f367'
            'e981ce26bb2394333c83512a607e8aa48ae0d66ec40e0f0b6d97ec70b6baa39f'
            '3ba9a85464e874c8ac4caeba155a217e34c3e78e85eccaeb3c2a331ed83882b3'
            '6b4a88fdfddd4c78c23cd8c26f5db1ca89ed6f1ae5558cf458a40482f6c64f98'
            '074690d913b9544bef11468454fbf5f52005b2a12160123340cfacc91d4daf9f'
            'f9953782524471c5a8ce819bf00bd47f8272cea17058d15f24522d01b5e827e5')
options=(!lto)
provides=('julia')
conflicts=('julia')


pkgver() {
  cd $_pkgbase

  # use the version from VERSION file
  ver=`git show makepkg:VERSION | sed 's/-/./g'`
  # Combine ver with rev-count and latest commit
  printf "%s.r%s.g%s" $(echo $ver) "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd $_pkgbase
  git submodule init
  git submodule update

# Update metadata install path
  patch -p1 -i ../julia-metainfo.patch
# Revert test that depends on patched gmp
  patch -Rp1 -i ../c12e8515.patch
# libgit2 1.8 compatibility
  patch -p1 -i ../julia-libgit2-1.8.patch
# libgit2 1.9 compatibility
  patch -p1 -i ../julia-libgit2-1.9.patch
# Don't hardcode library names
  patch -p1 -i ../julia-hardcoded-libs.patch
# Fix segfaults with curl 1.10
  #cd stdlib/srccache
  #_SAsha=89d3c7dded535a77551e763a437a6d31e4d9bf84
  #tar -xzf Downloads-$_SAsha.tar.gz
  #patch -d JuliaLang-Downloads.jl-${_SAsha:0:7} -p1 < "$srcdir"/julia-curl-1.10.patch
  #rm Downloads-$_SAsha.tar.gz
  #tar -czf Downloads-$_SAsha.tar.gz JuliaLang-Downloads.jl-${_SAsha:0:7}
  #md5sum Downloads-$_SAsha.tar.gz | cut -d ' ' -f 1 > ../../deps/checksums/Downloads-$_SAsha.tar.gz/md5
  #sha512sum Downloads-$_SAsha.tar.gz | cut -d ' ' -f 1 > ../../deps/checksums/Downloads-$_SAsha.tar.gz/sha512
}

_make() {
# Follow https://github.com/JuliaCI/julia-buildbot/blob/master/master/inventory.py for JULIA_CPU_TARGET
  local make_options=(
    prefix=/usr
    bindir=/usr/bin
    sysconfdir=/etc
    libexecdir=/usr/lib
    USE_BINARYBUILDER=0
    USE_SYSTEM_CSL=1
    USE_SYSTEM_LLVM=1
    USE_SYSTEM_LLD=1
    USE_SYSTEM_LIBUNWIND=1
    USE_SYSTEM_PCRE=1
    USE_SYSTEM_BLAS=1
    USE_SYSTEM_LAPACK=1
    USE_SYSTEM_LIBBLASTRAMPOLINE=1
    USE_SYSTEM_GMP=1
    USE_SYSTEM_MPFR=1
    USE_SYSTEM_LIBSUITESPARSE=1
    USE_SYSTEM_LIBWHICH=1
    USE_SYSTEM_DSFMT=0
    USE_SYSTEM_LIBUV=0
    USE_SYSTEM_UTF8PROC=1
    USE_SYSTEM_LIBGIT2=1
    USE_SYSTEM_LIBSSH2=1
    USE_SYSTEM_MBEDTLS=1
    USE_SYSTEM_CURL=0
    USE_SYSTEM_PATCHELF=1
    USE_SYSTEM_ZLIB=1
    USE_SYSTEM_P7ZIP=1
    USE_SYSTEM_OPENLIBM=1
    USE_BLAS64=1
    LIBBLAS=-lblas64
    LIBBLASNAME=libblas64
    LIBLAPACK=-llapack64
    LIBLAPACKNAME=liblapack64
    MARCH=x86-64
    JULIA_CPU_TARGET="generic;sandybridge,-xsaveopt,clone_all;haswell,-rdrnd,base(1)"
    VERBOSE=1
    JLDFLAGS="$LDFLAGS -lLLVM-16jl"
    LLVM_CONFIG=/usr/lib/llvm-julia/bin/llvm-config
  )

  LD_LIBRARY_PATH="/usr/lib/mbedtls2" make "${make_options[@]}" "$@"
}

build() {
  cd $_pkgbase
  PATH="$PATH:/usr/lib/llvm-julia/bin/" \
  _make release
}

check() {
  cd $_pkgbase/test
  ln -s /etc/ssl/cert.pem ../usr/share/julia

  ../julia --check-bounds=yes --startup-file=no ./runtests.jl \
    --skip cmdlineargs \
    --skip errorshow \
    --skip Downloads \
    --skip Sockets \
    --skip channels \
    --skip nghttp2_jll \
    --skip GMP_jll \
    --skip LibCURL \
    --skip LibSSH2_jll \
    --skip MbedTLS_jll \
    --skip MPFR_jll \
    --skip OpenBLAS_jll \
    --skip SuiteSparse_jll \
    --skip PCRE2_jll \
    --skip LibGit2_jll \
    --skip Zlib_jll
  find ../stdlib \( -name \*.cov -o -name \*.mem \) -delete
  rm -fr ../stdlib/Artifacts/test/artifacts
}

package() {
  cd $_pkgbase
  _make DESTDIR="$pkgdir" install
# Prevent compiled modules from being stripped, as it changes their checksum so Julia refuses to load them
  chmod -w "$pkgdir"/usr/share/julia/compiled/*/*/*.so

  ln -sf /etc/ssl/cert.pem "$pkgdir"/usr/share/julia # Needed by some packages

  rm "$pkgdir"/usr/lib/julia/libccalltest.so.debug # Remove debug testing library
  install -Dm644 LICENSE.md -t "$pkgdir"/usr/share/licenses/$pkgname

  install -Dm644 contrib/julia.svg -t "$pkgdir"/usr/share/pixmaps
}
