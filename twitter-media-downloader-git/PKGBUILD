# Maintainer: Nihal Kumar <2tv8xupqg at mozmail dot com>

pkgname=twitter-media-downloader-git
_pkgname=twitter-media-downloader
pkgver=r63.0cdd5e6
pkgrel=1
pkgdesc="A tool to download media from Twitter"
arch=('x86_64' 'i686' 'aarch64' 'armv7h')
url="https://github.com/mmpx12/twitter-media-downloader"
license=('unknown')
depends=('glibc')
makedepends=('git' 'go')
provides=("${_pkgname}")
conflicts=("${_pkgname}")
source=("${_pkgname}::git+https://github.com/mmpx12/twitter-media-downloader.git")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${_pkgname}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "${srcdir}/${_pkgname}"

  # Set Go build flags for reproducibility
  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"

  # Build directly with go instead of using Makefile
  go build -ldflags="-w -s" twmd.go
}

check() {
  cd "${srcdir}/${_pkgname}"
}

package() {
  cd "${srcdir}/${_pkgname}"

  # Install the binary manually since the Makefile doesn't support DESTDIR
  install -Dm755 twmd "${pkgdir}/usr/bin/twmd"

  if [ -f README.md ]; then
    install -Dm644 README.md "${pkgdir}/usr/share/doc/${_pkgname}/README.md"
  fi

  if [ -f LICENSE ]; then
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"
  fi
}
