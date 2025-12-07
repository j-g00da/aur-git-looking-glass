# Maintainer: Daniel Alejandro <dalejan051@gmail.com>

pkgname=simpmusic-bin
pkgver=1.0.0
pkgrel=4
pkgdesc="A FOSS YouTube Music client for Android and Desktop with many features from
Spotify, SponsorBlock, ReturnYouTubeDislike using Compose Multiplatform to develop."
arch=(x86_64)
url="https://www.simpmusic.org"
license=("GPL-3.0")

depends=("gstreamer" "gst-plugins-good" "gst-plugins-bad" "yt-dlp")
conflicts=("${pkgname%}")
options=("!strip" "!debug")

source=(
  "https://github.com/maxrave-dev/SimpMusic/releases/download/v${pkgver}/simpmusic_${pkgver}_amd64.deb"
)
sha256sums=("38c38ea1f70f48cad303e224bdad63fe595521aaa94cfb708defec2d179ce56b")

prepare() {
    bsdtar -xf data.tar.zst

    _basepath="${srcdir}/opt/simpmusic"
    # Add icon entry to .desktop
    grep -qfx "StartupWMClass=com-maxrave-simpmusic-MainKt" "${_basepath}/lib/simpmusic-SimpMusic.desktop" || \
    echo "StartupWMClass=com-maxrave-simpmusic-MainKt" >> "${_basepath}/lib/simpmusic-SimpMusic.desktop"
}

package() {
    # Install app
    cp -r --preserve=mode,timestamps opt/ "${pkgdir}/"

    _basepath="${pkgdir}/opt/simpmusic"

    # Install the icon
    if [[ -f "${srcdir}/opt/simpmusic/lib/SimpMusic.png" ]]; then
        install -Dm644 "${srcdir}/opt/simpmusic/lib/SimpMusic.png" \
            "${pkgdir}/usr/share/pixmaps/SimpMusic.png"
    fi

    # Install .desktop
    install -Dm644 "${_basepath}/lib/simpmusic-SimpMusic.desktop" \
        "${pkgdir}/usr/share/applications/simpmusic.desktop"

    # Permissions
    find "${pkgdir}" -type d -exec chmod 755 {} \;
    find "${pkgdir}" -type f -exec chmod 644 {} \;
    chmod 755 "${_basepath}/bin/SimpMusic" 2>/dev/null || true
}
