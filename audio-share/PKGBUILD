# Maintainer: A Farzat <a@farzat.xyz>
# Contributor: Zhanibek Adilbekov <zhnaibek.adilbekov@proton.me>
# shellcheck disable=2034,2154
pkgname=audio-share
pkgver=0.3.2
pkgrel=1
pkgdesc="Audio Share can share computer's audio to Android phone over network, so your phone becomes the speaker of computer"
arch=('x86_64')
url='https://github.com/mkckr0/audio-share'
license=('Apache-2.0')
depends=('libpipewire')
makedepends=('vcpkg' 'cmake' 'git')
source=("$pkgname-$pkgver.tar.gz::https://github.com/mkckr0/audio-share/archive/refs/tags/v${pkgver}.tar.gz"
        "git+https://github.com/microsoft/vcpkg")
b2sums=('19ad07d221b8726be03692aa027b8092d34dc2f699898197b650354713f46459832f05f5058938e79e0a529ea3429772bf6de5990901ea3f4be9b79c663e3cf6'
        'SKIP')

build() {
  export VCPKG_ROOT="$PWD/vcpkg"
  vcpkg install --downloads-root="$PWD/cache" --vcpkg-root="$VCPKG_ROOT" --binarysource=clear asio protobuf spdlog cxxopts
  cd "$pkgname-$pkgver/server-core"
  cmake --preset linux-Release
  cmake --build --preset linux-Release
}

package() {
  install -Dm755 "$srcdir/$pkgname-$pkgver/server-core/out/install/linux-Release/bin/as-cmd" "$pkgdir/usr/bin/as-cmd"
}

# vim: ts=2 sw=2 et
