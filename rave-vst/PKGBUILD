# Maintainer: aik2 aik2mlj@gmail.com

pkgname='rave-vst'
_name='rave-vst'
pkgdesc='VST audio effect and synthesizer based on RAVE, a variational autoencoder for fast and high-quality neural audio synthesis'
pkgver=0.0.2
pkgrel=1
groups=('vst3-plugins' 'pro-audio')
depends=('alsa-lib' 'freetype2' 'ttf-font' 'libx11')
makedepends=()
optdepends=()
provides=($_name)
conflicts=($_name)
arch=('x86_64')
url='https://forum.ircam.fr/projects/detail/rave-vst/'
license=('custom')

#Source file download guide
_sourcefile="./${_name}_${pkgver}_amd64.deb"
if [ ! -f ${_sourcefile} ]; then
    echo ""
    echo "	Due to license and website restriction, to install this package, the distribution file must be downloaded manually."
    echo "	You can download the source file of RAVE VST $pkgver from here:"
    echo ""
    echo "	https://forum.ircam.fr/asset/1650/${_name}_${pkgver}_amd64.deb"
    echo ""
    echo "	You must be logged in to the IRCAM forum in order to download"
    echo ""
    echo "	The Downloaded file must be placed in the appropriate directory depending on your AUR helper (or lack of thereof) here:"
    echo "		- makepkg: Same directory as this PKGBUILD"
    echo "		- yay: /home/<user>/.cache/yay/${pkgname}"
    echo "		- paru: /home/<user>/.cache/paru/clone/${pkgname}"
    echo ""
    echo "Operation Aborted"
    echo ""
    return 1
fi

source=("local://${_name}_${pkgver}_amd64.deb"
    "RAVE.desktop")
sha256sums=('d936f023467acd639b39e6faad9433adbdcee12a5fd184411907cab6b2b2998f'
    '12009284d625b3cb3a995a00cf835f55a9cdf0d14bb24f3a99cef527f141e081')

package() {
    tar -xf data.tar.xz --no-same-owner -C "${pkgdir}"

    # Fix directory permissions
    find "$pkgdir/usr" -type d -exec chmod 755 {} +

    # custom desktop file
    install -Dm644 "RAVE.desktop" "${pkgdir}/usr/share/applications/RAVE.desktop"

    # move folders for conventions
    mv "${pkgdir}/usr/lib/vst" "${pkgdir}/usr/lib/vst3"
    mv "${pkgdir}/usr/share/icons" "${pkgdir}/usr/share/pixmaps"
}
