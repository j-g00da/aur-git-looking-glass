# Maintainer: Oreste Sciacqualegni <giulianoverrando@gmail.com>

pkgname=brother-mfcj6940dw-bin
pkgver=3.5.0
pkgrel=1
pkgdesc="LPR driver and CUPS wrapper for Brother MFC-J6940DW printer"
arch=("i686" "x86_64")
url="https://support.brother.com/g/b/producttop.aspx?c=eu_ot&lang=en&prod=mfcj6940dw_us_eu_as"
license=("EULA")
groups=("base-devel")
source=("https://download.brother.com/welcome/dlf105465/mfcj6940dwpdrv-$pkgver-1.i386.deb")
md5sums=('7d2f33b2dc5e72b428665b7628fd9d83')
depends=('bash' 'glibc' 'perl' 'lib32-glibc')

package() {
	tar -xf data.tar.gz -C "${pkgdir}"
}

