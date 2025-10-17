pkgname=uaspl
pkgver=1.2.2
pkgrel=2
pkgdesc="Utilidad Automatizada para la Seguridad y Protección en Linux"
arch=('any')
url="https://github.com/KevinCrrl/UASPL"
license=('GPL3')
source=("https://github.com/KevinCrrl/UASPL/releases/download/${pkgver}/UASPL-${pkgver}.tar.xz")
sha256sums=("0761fd9c04203002b262a7901c4449c05577971e345a8afc25efcd0c67f6810c")
conflicts=('uaspl-bin')
depends=(
    'python'
    'python-customtkinter'
    'python-pyxdg'
    'python-colorama'
    'python-jsonschema'
    'python-pyfiglet'
    'clamav'
    'rkhunter'
    'ufw'
)
makedepends=(
    'python-build'
    'python-installer'
    'python-wheel'
)

build() {
    cd "${srcdir}/UASPL-${pkgver}"
    python -m build --wheel --no-isolation
}

package() {
    cd "${srcdir}/UASPL-${pkgver}"
    python -m installer --destdir="$pkgdir" dist/*.whl
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}