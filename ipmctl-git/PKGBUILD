# Maintainer: fft
# Contributor: Jianqiu Zhang <void001@archlinuxcn.org>

pkgname=ipmctl-git
pkgver=v03.00.00.0485.2.r5.gd2caed16
pkgrel=2
pkgdesc="util for configuring and managing Intel Optane DC persistent memory modules (DCPMM)."
arch=('x86_64')
url="https://github.com/intel/ipmctl"
license=('BSD-3-Clause')
depends=("ndctl")
makedepends=("asciidoctor" "cmake" "git" "python3" "patch")

source=(
  ${pkgname}::git+https://github.com/intel/ipmctl
  edk2::git+https://github.com/tianocore/edk2.git
  p1.patch
  p2.patch
  p3.patch
)

sha256sums=(
  'SKIP'
  'SKIP'
  '7a25005dddf360cb6068905be30b1698f49ca3bf6c57ea1395c3c1d3ddde0405'
  'a0397145e1e278ae2c81c256d6dae34efad45d7645e8b121417e864f6512ca49'
  '230107ca256039261fe1801b10c5427e52c626c03b1fcb97a49ea413d959f6f6'
)

pkgver() {
  cd "${srcdir}/${pkgname}"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  cd "${pkgname}"
  ./updateedk.sh
  git apply ../../p1.patch #fixed version of src/os/patches/0001-Ignore-STATIC_ASSERTs-and-NULL-define-for-os-and-ut-builds.patch
  git apply ../../p2.patch #https://github.com/intel/ipmctl/issues/192
  git apply ../../p3.patch #https://github.com/tianocore/edk2/issues/10466
}

build() {
  cd "${srcdir}/${pkgname}"
  mkdir -p build && cd build
  cmake -DCMAKE_POLICY_VERSION_MINIMUM=3.5 -DRELEASE=ON -DCMAKE_INSTALL_PREFIX="/usr" ..
  cmake --build ./
}

package() {
  cd "${srcdir}/${pkgname}/build"
  cmake --build ./ --target install DESTDIR="${pkgdir}"
  mv "${pkgdir}/usr/etc" "${pkgdir}/etc"
  rm -r "${pkgdir}/usr/var" "${pkgdir}/usr/share/doc/ipmctl/LICENSE"
  install -Dm644 "${srcdir}/${pkgname}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:

