# Maintainer: Greg Land <landjgregory@gmail.com>
pkgname=alacritty-theme-autocomplete-git
pkgrel=1
pkgdesc="Just simple scripts to handle alacritty color schemes."
pkgver=r1.c68ed3e
arch=('any')
url="https://github.com/GregoryLand/alacritty-theme-autocomplete"
license=('MIT')
makedepends=('git')
depends=('alacritty-theme-git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
options=(!debug)
source=('alacritty-theme-autocomplete::git+https://github.com/GregoryLand/alacritty-theme-autocomplete#branch=master')
noextract=()
sha256sums=('SKIP')

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
        cd "$srcdir/${pkgname%-git}"
        install -Dm 555 alacritty-theme "$pkgdir/usr/bin/alacritty-theme"
        install -Dm 444 alacritty-themes.bash "$pkgdir/etc/bash_completion.d/alacritty-themes.bash"
}

