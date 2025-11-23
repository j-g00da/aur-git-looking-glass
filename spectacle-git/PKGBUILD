# Maintainer:
# Contributor: katt <magunasu.b97@gmail.com>
# Contributor: FadeMind <fademind@gmail.com>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

_pkgname="spectacle"
pkgname="$_pkgname-git"
pkgver=6.5.2.r31.g7f6745a
pkgrel=1
epoch=1
pkgdesc='KDE screenshot capture utility'
url='https://invent.kde.org/graphics/spectacle'
license=('GPL-2.0-or-later')
arch=('x86_64')

depends=(
  'kcrash'
  'kpipewire'
  'kstatusnotifieritem'
  'layer-shell-qt'
  'opencv'
  'prison'
  'purpose'
  'qt6-multimedia'
  'xcb-util-cursor'
  'zxing-cpp'
)
makedepends=(
  'extra-cmake-modules'
  'git'
  'kdoctools'
  'ninja'
  'plasma-wayland-protocols'
)

provides=("$_pkgname")
conflicts=("$_pkgname")

_pkgsrc="$_pkgname"
source=("$_pkgsrc"::"git+$url.git")
sha256sums=('SKIP')

pkgver() {
  cd "$_pkgsrc"
  local _regex _file _line _line_num _version _commit _revision _hash
  _regex='^\s+<release version="([0-9]+\.[0-9]+(\.[0-9]+)?)".*>$'
  _file='desktop/org.kde.spectacle.appdata.xml'

  _line=$(grep -E "$_regex" "$_file" | head -1)
  _line_num=$(grep -Ensm1 "$_regex" "$_file" | cut -d':' -f1)

  _version=$(sed -E "s@$_regex@\1@" <<< "$_line")
  _commit=$(git blame -L $_line_num,+1 -- "$_file" | awk '{print $1;}')
  _revision=$(git rev-list --count --cherry-pick "$_commit"...HEAD)
  _hash=$(git rev-parse --short=7 HEAD)

  printf '%s.r%s.g%s' "${_version:?}" "${_revision:?}" "${_hash:?}"
}

build() {
  local _cmake_options=(
    -B "build"
    -S "$_pkgsrc"
    -G Ninja
    -DCMAKE_BUILD_TYPE=None
    -DCMAKE_INSTALL_PREFIX=/usr
    -DBUILD_TESTING=OFF
    -Wno-dev
  )

  cmake "${_cmake_options[@]}"
  cmake --build "build"
}

package() {
  DESTDIR="$pkgdir" cmake --install "build"
}
