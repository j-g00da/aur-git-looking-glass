# Maintainer: aik2 <aik2mlj@gmail.com>

_name=otf-librebaskerville
pkgname=$_name-git
pkgver=r93.f48a4a5
pkgrel=1
pkgdesc="Libre Baskerville is webfont optimized for web body text (typically 16px). It's based on 1941 ATF Specimens, but it has a taller x height, wider counters and minor contrast that allow it to work on small sizes in any screen."
arch=("any")
url="http://www.impallari.com/projects/overview/libre-baskerville"
license=("custom:OFL")
makedepends=(git)
source=("$_name::git+https://github.com/impallari/Libre-Baskerville.git")
provides=($_name)
conflicts=($_name)
sha256sums=('SKIP')

pkgver() {
    cd $_name
    (
        set -o pipefail
        git describe --long --abbrev=7 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
            printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
    )
}

package() {
    cd $_name

    install -Dm644 fonts/LibreBaskerville-*.otf -t "${pkgdir}/usr/share/fonts/OTF/"

    # Licence installation
    install -Dm644 "OFL.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
