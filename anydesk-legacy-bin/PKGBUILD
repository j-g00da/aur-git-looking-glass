# Maintainer: Microck <contact@micr.dev>
# Project Page: https://github.com/Microck/anydesk-legacy-bin

pkgname=anydesk-legacy-bin
pkgver=6.0.1
pkgrel=2
pkgdesc="Legacy AnyDesk 6.0.1. Stable version without commercial use nags or timeouts."
arch=('x86_64')
url="https://www.anydesk.com"
license=('custom')

depends=('gtk2' 'gtkglext' 'glu' 'cairo' 'fontconfig' 'freetype2' 
         'gdk-pixbuf2' 'glib2' 'libglvnd' 'libice' 'libsm' 
         'libx11' 'libxtst' 'pango' 'pangox-compat' 'lsb-release' 'polkit')

optdepends=('xdg-utils: for desktop integration'
            'gtk-engine-murrine: fixes GTK theme warnings and improves look')

conflicts=('anydesk' 'anydesk-bin')
provides=('anydesk')

options=('!strip' '!emptydirs')
install=${pkgname}.install

source=("anydesk-${pkgver}.deb::https://web.archive.org/web/20230419070452if_/https://download.anydesk.com/linux/deb/anydesk_6.0.1-1_amd64.deb")
sha512sums=('9ff2d5fe2d87e06f2860fc1759af3b1b10749feb3a97023905a314047e42e805028619f81a4d541cd3fd0ffab8bec71965e191a3d295d745f7738b150c53fc69')

package(){
    tar -x -f data.tar.* -C "${pkgdir}"

    _copyright_file=$(find "${pkgdir}" -name "copyright" -print -quit)
    
    if [ -n "$_copyright_file" ]; then
        install -Dm644 "$_copyright_file" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    else
        msg "Warning: No copyright file found. Skipping license installation."
    fi
    
    if [ -f "${pkgdir}/usr/bin/anydesk" ]; then
        chmod 755 "${pkgdir}/usr/bin/anydesk"
    fi
}
