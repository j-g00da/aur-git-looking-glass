# Maintainer: Iyán Méndez Veiga <me (at) iyanmv (dot) com>
_pkgname=pyqcc
pkgname=python-${_pkgname}
pkgver=0.1.4
pkgrel=1
pkgdesc="Python package to communicate with Crypta Labs QRNG devices"
arch=(any)
url=https://cryptalabs.com/qrng-driver-downloads/
license=(LicenseRef-unknown)
depends=(
    python
    python-pyserial
    qcc
)
makedepends=(python-installer)
source=(
    https://cryptalabs.com/support/releases/pyqcc/$_pkgname-$pkgver-py3-none-$arch.whl
    license-unknown.txt
)
b2sums=('ca7be7578738abcc97929c44cf0f5fc90b80593db7bc978d0c00a9ef277f9ec599d2ec4d2fbd7e02e7576d3ab6dcdbfd6d0ca9e7831a455424b1c21b7da05e60'
        '900dfce730c0f29b0cd5fafdf5ed6bc08a3ca245c3bbee12878c7e183951e0a55e33205da747d1666baded6133473fa8506dea252a2bc23f6f7555ebfa500d54')

package() {
    python -m installer --destdir="$pkgdir" *.whl
    install -D -m0644 license-unknown.txt "$pkgdir"/usr/share/licenses/$pkgname/license-unknown.txt
}
