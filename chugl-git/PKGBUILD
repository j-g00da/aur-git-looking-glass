# Maintainer: aik2 <aik2mlj@gmail.com>

pkgname=chugl-git
_name=chugl
pkgdesc="ChuGL => ChucK Graphics Library"
pkgver=0.2.4.r0.g6c8e36e
pkgrel=1
arch=(x86_64)
url="https://chuck.stanford.edu/chugl/"
license=(MIT)
depends=(chuck)
groups=(pro-audio multimedia)
makedepends=(git cmake)
source=("$_name::git+https://github.com/ccrma/chugl.git")
provides=($_name)
conflicts=($_name)
sha256sums=("SKIP")

pkgver() {
  cd $_name
  # printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  git describe --long --tags --abbrev=7 | sed "s/\([^-]*-g\)/r\1/;s/-/./g" | sed "s/^v//g"
}

build() {
  cd "$_name/src"
  make linux
}

package() {
  cd $_name
  install -d "$pkgdir/usr/share/doc/$_name"
  cp -r examples "$pkgdir/usr/share/doc/$_name"
  install -d "$pkgdir/usr/lib/chuck/"
  install -Dm755 src/ChuGL.chug "$pkgdir/usr/lib/chuck/ChuGL.chug"
}
