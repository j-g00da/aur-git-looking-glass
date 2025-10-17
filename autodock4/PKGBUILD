# Maintainer: Andrew <andrewforlua@gmail.com>
pkgname=autodock4
pkgver=4.2.6
pkgrel=2
pkgdesc="Automated docking of flexible ligands to proteins"
arch=('x86_64' 'i686')
url="https://github.com/ccsb-scripps/AutoDock4"
license=('GPL')
depends=('gcc-libs')
makedepends=('gcc' 'make' 'tcsh' 'autoconf' 'automake')
source=("autodock4-$pkgver.tar.gz::https://github.com/ccsb-scripps/AutoDock4/archive/refs/heads/master.tar.gz"
        "autogrid4-$pkgver.tar.gz::https://github.com/ccsb-scripps/AutoGrid/archive/refs/heads/master.tar.gz")
sha256sums=('1c44e7b6f0ea8a59aae8f4701ad5cbaa4c1b55e32549d3189af663349126b834'
            'd3eed098d75a7d7189e9986f575ab7eff12fd932abb57005831f64b763a450fa')

build() {
    # Build AutoDock4
    cd "$srcdir/AutoDock4-master"
    
    echo "==> Configuring AutoDock..."
    autoreconf -i
    ./configure --prefix=/usr
    
    echo "==> Building AutoDock..."
    make
    
    # Build AutoGrid4
    cd "$srcdir/AutoGrid-master"
    
    echo "==> Configuring AutoGrid..."
    autoreconf -i
    ./configure --prefix=/usr
    
    echo "==> Building AutoGrid..."
    make
}

package() {
    # Install AutoDock binary
    install -Dm755 "$srcdir/AutoDock4-master/autodock4" "$pkgdir/usr/bin/autodock4"
    
    # Install AutoGrid binary
    install -Dm755 "$srcdir/AutoGrid-master/autogrid4" "$pkgdir/usr/bin/autogrid4"
    
    # Install documentation
    install -Dm644 "$srcdir/AutoDock4-master/README" "$pkgdir/usr/share/doc/$pkgname/README"
    install -Dm644 "$srcdir/AutoDock4-master/COPYING" "$pkgdir/usr/share/doc/$pkgname/COPYING"
}