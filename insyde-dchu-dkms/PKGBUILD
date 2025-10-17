pkgname=insyde-dchu-dkms
pkgver=0.1.0
pkgrel=1
pkgdesc='Insyde DCHU MFD (CLV0001) with hwmon + LED drivers (DKMS)'
arch=('x86_64')
url='https://github.com/hUwUtao/opendchu'
license=('0BSD')
depends=('dkms')
provides=('insyde-dchu')
conflicts=('insyde-dchu')
options=('!strip')

_modsrc="/usr/src/${pkgname}-${pkgver}"

# Package local sources so makepkg can stage them in $srcdir
source=(
  'dchu_core.c'
  'dchu_hwmon.c'
  'dchu_leds.c'
  'dchu.h'
  'Makefile'
  'dkms.conf'
  'README.md'
  'glow_kbd.sh'
)
sha256sums=(
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
)

package() {
  install -d "${pkgdir}${_modsrc}"

  # Core sources
  install -m644 "$srcdir/dchu_core.c" "${pkgdir}${_modsrc}/"
  install -m644 "$srcdir/dchu_hwmon.c" "${pkgdir}${_modsrc}/"
  install -m644 "$srcdir/dchu_leds.c" "${pkgdir}${_modsrc}/"
  install -m644 "$srcdir/dchu.h" "${pkgdir}${_modsrc}/"
  install -m644 "$srcdir/Makefile" "${pkgdir}${_modsrc}/"
  install -m644 "$srcdir/dkms.conf" "${pkgdir}${_modsrc}/"
  install -m644 "$srcdir/README.md" "${pkgdir}${_modsrc}/" || true

  # Optional helper script
  install -d "${pkgdir}/usr/bin"
  install -m755 "$srcdir/glow_kbd.sh" "${pkgdir}/usr/bin/insyde-dchu-glow" || true

  # Auto-load modules on boot
  install -d "${pkgdir}/usr/lib/modules-load.d"
  printf '%s\n' \
    'dchu_core' \
    'dchu_hwmon' \
    'dchu_leds' \
    > "${pkgdir}/usr/lib/modules-load.d/insyde-dchu.conf"
}
