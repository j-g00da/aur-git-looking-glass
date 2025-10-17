# Maintainer: Jonas Bögle <aur@iwr.sh>

pkgname=yass-reloaded
pkgver=2025.8
pkgrel=1
pkgdesc="Editor for creating, fine-tuning, organizing and printing Ultrastar karaoke songs"
arch=('i686' 'x86_64')
url="https://github.com/DoubleDee73/Yass"
license=('GPL')
depends=('jdk-openjdk>=24' 'java-openjfx>=24' 'gtk2' 'bash')
makedepends=('unzip')
_filename="Yass-Reloaded-${pkgver}.jar"
source=(
	"https://github.com/DoubleDee73/Yass/releases/download/${pkgver}/${_filename}"
	"${pkgname}.desktop"
	"${pkgname}.sh")
sha256sums=('999852ec9a1a459b0e83d9314abf902c8f779f9b0b8ff89f3e33ea063e7dcea8'
            '3302b96b565e374f6de96c7139407bf8ee7b4bc206405f7489ee2cb109a57382'
            'b5111811746c39ccab9b1d65ff4db2456127b38dfeeafcb97d184d2e12ee4ba6')
options=(!strip)
noextract=("${_filename}")

package() {
	# jar
	install -Dm644 "${srcdir}/${_filename}" "${pkgdir}/usr/share/java/${pkgname}.jar"
	# icon
	unzip -j -d "${srcdir}" -o "${_filename}" yass/resources/icons/yass-icon.png
	install -Dm644 "${srcdir}/yass-icon.png" "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
	# desktop
	install -Dm644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
	# launch script
	install -dm755 "${pkgdir}/usr/bin"
	install -m755 "${srcdir}/${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
}
