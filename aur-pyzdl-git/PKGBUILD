# Maintainer: Jake Goritski (jgoritski@gmail.com)
pkgname="pyzdl"
pkgbase="aur-pyzdl-git"
pkgver="1.0.0"
pkgrel=1
pkgdesc="Doom launcher in Python"
arch=("x86_64")
depends=("python-wxpython")
license=("MIT")
source=("git+https://github.com/drproteus/pyzdl.git")
sha512sums=("SKIP")
package() {
  mkdir -p "${pkgdir}/usr/bin"
  mkdir -p "${pkgdir}/usr/share/pyzdl"
  cp -av "${srcdir}/pyzdl" "${pkgdir}/usr/share/."
  echo "#!/bin/bash" >> "${pkgdir}/usr/bin/pyzdl"
  echo "python ${pkgdir}/usr/share/pyzdl/gui.py" >> "${pkgdir}/usr/bin/pyzdl"
  chmod +x "${pkgdir}/usr/bin/pyzdl"
}

