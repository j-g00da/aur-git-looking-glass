# Maintainer: Kiet "Shihotori" Huynh <11086238+superkidvn@users.noreply.github.com>
pkgname=whitesur-kde-theme
_gitname=WhiteSur-kde
pkgver=2024.11.18
pkgrel=2
pkgdesc="MacOS Big Sur theme for KDE Plasma"
arch=(any)
url="https://github.com/vinceliuice/${_gitname}"
license=('GPL-3.0')
optdepends=(
  'kvantum: Kvantum theme support'
  'sddm: SDDM theme support'
  'whitesur-icon-theme: Whitesur icon theme'
  'whitesur-cursor-theme: Whitesur cursor theme'
)
provides=(
  'kvantum-theme-whitesur'
  'whitesur-kvantum-theme'
)
conflicts=(
  'kvantum-theme-whitesur'
  'whitesur-kvantum-theme'
  'plasma5-themes-whitesur'
)
install=post_install.install
source=("${pkgname}-${pkgver//./-}.tar.gz::${url}/archive/refs/tags/${pkgver//./-}.tar.gz")
sha256sums=('8ab21920e8df0647431b7f23ace7f9a7a51b320263f4364ac286bae1a359e91a')

package() {
  # Variables
  _auroraedir="${pkgdir}/usr/share/aurorae/themes"
  _schemesdir="${pkgdir}/usr/share/color-schemes"
  _plasmadir="${pkgdir}/usr/share/plasma/desktoptheme"
  _lookfeeldir="${pkgdir}/usr/share/plasma/look-and-feel"
  _kvantumdir="${pkgdir}/usr/share/Kvantum"
  _wallpaperdir="${pkgdir}/usr/share/wallpapers"
  _sddmdir="${pkgdir}/usr/share/sddm/themes"
  _extractdir="${srcdir}/${_gitname}-${pkgver//./-}"
  _pcolors=(
    ""
    "-alt"
    "-dark"
  )
  _lights=(
    "${_gitname%-kde}"
    "${_gitname//kde/sharp}"
    "${_gitname//kde/opaque}"
  )
  _darks=(
    "${_gitname//kde/dark}"
    "${_gitname//kde/dark-sharp}"
    "${_gitname//kde/dark-opaque}"
  )
  _scales=(
    ""
    "_x1.25"
    "_x1.5"
    "_x1.75"
    "_x2.0"
  )
  _aurorae_light_names=()
  _aurorae_dark_names=()

  for _scale in "${_scales[@]}"; do
    for _light in "${_lights[@]}"; do
      _aurorae_light_names+=("${_light}${_scale}")
    done
    for _dark in "${_darks[@]}"; do
      _aurorae_dark_names+=("${_dark}${_scale}")
    done
  done

  # Create directories
  install -d \
    "${_auroraedir}" \
    "${_schemesdir}" \
    "${_plasmadir}" \
    "${_lookfeeldir}" \
    "${_kvantumdir}" \
    "${_wallpaperdir}" \
    "${_sddmdir}"
 
 # Install Kvantum theme and wallpaper
  cp -r "${_extractdir}/Kvantum/"* "${_kvantumdir}"
  cp -r "${_extractdir}/wallpaper/"* "${_wallpaperdir}"

  # Install plasma theme and color scheme
  cp -r "${_extractdir}/color-schemes/"* "${_schemesdir}"
  cp -r "${_extractdir}/plasma/desktoptheme/${_gitname%-kde}"* "${_plasmadir}"
  cp -r "${_extractdir}/plasma/look-and-feel/"* "${_lookfeeldir}"

  # Install aurorae
  cp -r "${_extractdir}/aurorae/"{main,main-opaque,main-sharp}/* "${_auroraedir}"

  for _aurorae_light_name in "${_aurorae_light_names[@]}"; do
    cp -r "${_extractdir}/aurorae/common/assets/"* "${_auroraedir}/${_aurorae_light_name}"
    cp -r "${_extractdir}/aurorae/"{metadata.desktop,metadata.json} "${_auroraedir}/${_aurorae_light_name}"
    cp -r "${_auroraedir}/${_aurorae_light_name%_x*}rc" "${_auroraedir}/${_aurorae_light_name}/${_aurorae_light_name}rc"
    sed -i "s/${_gitname%-kde}/${_aurorae_light_name}/g" \
      "${_auroraedir}/${_aurorae_light_name}/metadata.desktop" \
      "${_auroraedir}/${_aurorae_light_name}/metadata.json"
  done

  for _aurorae_dark_name in "${_aurorae_dark_names[@]}"; do
    cp -r "${_extractdir}/aurorae/common/assets-dark/"* "${_auroraedir}/${_aurorae_dark_name}"
    cp -r "${_extractdir}/aurorae/"{metadata.desktop,metadata.json} "${_auroraedir}/${_aurorae_dark_name}"
    cp -r "${_auroraedir}/${_aurorae_dark_name%_x*}rc" "${_auroraedir}/${_aurorae_dark_name}/${_aurorae_dark_name}rc"
    sed -i "s/${_gitname%-kde}/${_aurorae_dark_name}/g" \
      "${_auroraedir}/${_aurorae_dark_name}/metadata.desktop" \
      "${_auroraedir}/${_aurorae_dark_name}/metadata.json"
  done

  # Clean up redundant aurorae rc files
  rm -f "${_auroraedir}/${_gitname%-kde}"*rc

  # Install sddm theme
  for i in {"-light","-dark"}; do
    cp -r "${_extractdir}/sddm/${_gitname%-kde}-6.2" "${_sddmdir}/${_gitname%-kde}${i}"
    cp -r "${_extractdir}/sddm/images/background$i.jpeg" "${_sddmdir}/${_gitname%-kde}${i}/background.jpeg"
    cp -r "${_extractdir}/sddm/images/preview$i.jpeg" "${_sddmdir}/${_gitname%-kde}${i}/preview.jpeg"

    sed -i "/\Name=/s/${_gitname%-kde}/${_gitname%-kde}${i}/" "${_sddmdir}/${_gitname%-kde}${i}/metadata.desktop"
    sed -i "/\Theme-Id=/s/${_gitname%-kde}/${_gitname%-kde}${i}/" "${_sddmdir}/${_gitname%-kde}${i}/metadata.desktop"
    sed -i "s/${_gitname%-kde}/${_gitname%-kde}${i}/g" "${_sddmdir}/${_gitname%-kde}${i}/Main.qml"
  done

  # Install license
  install -Dm0644 -t "${pkgdir}/usr/share/licenses/${pkgname}" "${_extractdir}/LICENSE" 
}
