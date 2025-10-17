# Maintainer: Winston Astrachan <rew1red [at] rew1 [dot] red>

pkgname=brother-mfc-l3780cdw
pkgver=3.5.1_1
pkgrel=3
pkgdesc="LPR and CUPS driver for the Brother MFC-L3780CDW"
arch=('x86_64')
url="https://support.brother.com/g/b/downloadend.aspx?c=us&lang=en&prod=mfcl3780cdw_us_as&os=128&dlid=dlf105764_000&flang=4&type3=10283"
license=('LicenseRef-brother')
depends=('cups' 'ghostscript' 'perl' 'lib32-glibc')
optdepends=('brscan4: scanner support')
_pkgfilename="mfcl3780cdwpdrv-${pkgver/_/-}.i386.deb"
source=("https://download.brother.com/welcome/dlf105764/${_pkgfilename}")
sha256sums=('0973b0836578c0c3b55298b07046a86d5c57eea9d7118d20f06cfb68bc35ffec')

package(){
    tar -xaf "${srcdir}/data.tar.gz" -C "${pkgdir}/"
    cd "${pkgdir}/opt/brother/Printers/mfcl3780cdw"

    # copy cups filters out of architecture-specific directories  (from .deb postinst)
    cp "lpd/x86_64/brmfcl3780cdwfilter" \
       "lpd/brmfcl3780cdwfilter"
    cp "lpd/x86_64/brprintconf_mfcl3780cdw" \
       "lpd/brprintconf_mfcl3780cdw"
    rm -rf "lpd/i686"
    rm -rf "lpd/x86_64"

    # symlink cupswrapper files
    install -d "${pkgdir}/usr/lib/cups/filter/"
    ln -sf "/opt/brother/Printers/mfcl3780cdw/cupswrapper/brother_lpdwrapper_mfcl3780cdw" \
           "${pkgdir}/usr/lib/cups/filter/"

    # symlink cups ppd files
    install -d "${pkgdir}/usr/share/cups/model/"
    ln -sf "/opt/brother/Printers/mfcl3780cdw/cupswrapper/brother_mfcl3780cdw_printer_en.ppd" \
           "${pkgdir}/usr/share/cups/model/"

    # install license files
    install -Dm644 LICENSE_ENG.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE_ENG.txt"
}
