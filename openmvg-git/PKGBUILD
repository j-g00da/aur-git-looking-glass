# Maintainer: Kyle Brooks <brookskd@gmail.com>
# Submaintainer : bartus <arch-user-repoᘓbartus.33mail.com>
# shellcheck disable=SC2034,SC2164

pkgname=openmvg-git
_gitname='openMVG'
_fragment="#branch=develop"
pkgver=2.0.r114.gc92ed1be
pkgrel=1
pkgdesc='open Multiple View Geometry library. Basis for 3D computer vision and Structure from Motion.'
arch=('i686' 'x86_64')
url='http://imagine.enpc.fr/~moulonp/openMVG/'
license=('MPL')
options=('!emptydirs')
depends=(qt5-{base,svg} 'cereal' 'glfw' 'lz4' 'libpng' 'libjpeg' 'libtiff' 'libxcursor' 'libxinerama' 'libxrandr' 'libxxf86vm' 'libxi' 'graphviz' 'libgl' 'ceres-solver' 'gflags' 'flann' 'coin-or-coinutils' 'coin-or-clp' 'coin-or-osi' 'coin-or-lemon')
makedepends=('git' 'cmake' 'doxygen' 'eigen3')
source=("git+https://github.com/${_gitname}/${_gitname}.git${_fragment}"
       )
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            'SKIP')
b2sums=('SKIP'
        'SKIP'
        'SKIP'
        'SKIP')

pkgver() {
  git -C "${srcdir}/${_gitname}" describe --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  prepare_submodule
}

build() {
  cmake -S "${srcdir}/${_gitname}"/src -B build \
        -DCMAKE_POLICY_VERSION_MINIMUM=3.5 \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_BUILD_TYPE=RELEASE \
        -DOpenMVG_BUILD_SHARED=ON \
        -DOpenMVG_BUILD_EXAMPLES=ON \
        -DOpenMVG_BUILD_OPENGL_EXAMPLES=ON \
        -DOpenMVG_USE_OPENMP=ON \
        -DCOINUTILS_INCLUDE_DIR_HINTS=/usr/include/coin \
        -DCLP_INCLUDE_DIR_HINTS=/usr/include/coin \
        -DOSI_INCLUDE_DIR_HINTS=/usr/include/coin \
        -DLEMON_INCLUDE_DIR_HINTS=/usr/include/lemon \
        -DCERES_DIR_HINTS=/usr/include/ceres
  cmake --build build
}

package() {
  DESTDIR="$pkgdir"  cmake --install build
}

# Generated with git_submodule_PKGBUILD_conf.sh ( https://gist.github.com/bartoszek/41a3bfb707f1b258de061f75b109042b )
# Call prepare_submodule in prepare() function

prepare_submodule() {
  git -C "$srcdir/openMVG" config submodule.src/dependencies/glfw.url "$srcdir/glfw"
  git -C "$srcdir/openMVG" config submodule.src/dependencies/osi_clp.url "$srcdir/osi_clp"
  git -C "$srcdir/openMVG" config submodule.src/dependencies/cereal.url "$srcdir/cereal"
  git -C "$srcdir/openMVG" -c protocol.file.allow=always submodule update --init
}
source+=(
  "glfw::git+https://github.com/elmindreda/glfw"
  "osi_clp::git+https://github.com/openMVG-thirdparty/osi_clp"
  "cereal::git+https://github.com/openMVG-thirdparty/cereal"
)
# vim:set ts=2 sw=2 et:
