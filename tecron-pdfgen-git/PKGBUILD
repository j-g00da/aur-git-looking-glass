# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# The following guidelines are specific to BZR, GIT, HG and SVN packages.
# Other VCS sources are not natively supported by makepkg yet.

# Maintainer: Your Name <youremail@domain.com>
pkgname=tecron-pdfgen-git # '-bzr', '-git', '-hg' or '-svn'
pkgver=v0.0.3.r1.ecf583a
pkgrel=3
pkgdesc="Python helper for downloading pdf documents for people working in Tecrom"
arch=(x86_64)
url=""
license=('GPL')
makedepends=(
	git 
	python-build 
	python-installer 
	python-wheel 
	python-setuptools
) # 'bzr', 'git', 'mercurial' or 'subversion'
provides=("${pkgname%-VCS}")
conflicts=("${pkgname%-VCS}")
replaces=()
backup=()
options=()
install=
url=https://www.aivallecrosia.com
source=('git+https://github.com/AI-Vallecrosia/tecron-pdfgen.git')
noextract=()
depends=(
	python-playwright 
	python-pypdf2 
	python-requests
    python-beautifulsoup4
	tk
)
sha256sums=('SKIP')

# Please refer to the 'USING VCS SOURCES' section of the PKGBUILD man page for
# a description of each element in the source array.

pkgver() {
	cd "$srcdir/tecron-pdfgen"

# The examples below are not absolute and need to be adapted to each repo. The
# primary goal is to generate version numbers that will increase according to
# pacman's version comparisons with later commits to the repo. The format
# VERSION='VER_NUM.rREV_NUM.HASH', or a relevant subset in case VER_NUM or HASH
# are not available, is recommended.

# Git, tags available
	printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}


build() {
	cd "$srcdir/tecron-pdfgen"
	python -m build --wheel --no-isolation
}

package() {
	cd "$srcdir/tecron-pdfgen"
	python -m installer --destdir="$pkgdir" dist/*.whl
    install -Dm644 "tecron-genpdf.desktop" -t "$pkgdir/usr/share/applications/"
	for size in 16 32 48 64 128; do
    	if [ -f "assets/tecron-genpdf_${size}x${size}.png" ]; then
      		install -Dm644 "assets/tecron-genpdf_${size}x${size}.png" \
        	"$pkgdir/usr/share/icons/hicolor/${size}x${size}/apps/tecron-pdfgen.png"
    	fi
  	done
	if [ -z "${XDG_DATA_HOME}" ]; then
		DATA_DIR="${HOME}/.local/share"
	else 
		DATA_DIR="${XDG_DATA_HOME}"
	fi
	if [ ! -d "$DATA_DIR/tecron_pdfgen" ]; then
		mkdir -p "$DATA_DIR/tecron_pdfgen"
	fi
	if [ ! -f "$DATA_DIR/tecron_pdfgen/password.secret" ]; then
		touch "$DATA_DIR/tecron_pdfgen/password.secret"
		chmod 600 "$DATA_DIR/tecron_pdfgen/password.secret"
	fi	
}
