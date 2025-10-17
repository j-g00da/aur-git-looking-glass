pkgname=yandex-music-bin
pkgver=5.73.1     # текущая версия приложения
https://music-desktop-application.s3.yandex.net/stable/Yandex_Music_amd64_5.73.1.deb
pkgrel=1
pkgdesc="Yandex Music desktop (repacked from .deb)"
arch=('x86_64')
url="https://music.yandex.ru/"
license=('custom')
depends=(
  'gtk3'
  'libnotify'
  'nss'
  'libxss'
  'libxtst'
  'xdg-utils'
  'at-spi2-core'
  'util-linux-libs'
  'libsecret'
  'hicolor-icon-theme'
)

optdepends=(
  'libappindicator-gtk3: системный индикатор в трее'
)

provides=('yandex-music')
conflicts=('yandex-music')

options=('!strip' '!debug')

# кладём .deb рядом с PKGBUILD
source=("https://music-desktop-application.s3.yandex.net/stable/Yandex_Music_amd64_${pkgver}.deb")
noextract=("Yandex_Music_amd64_${pkgver}.deb")
sha256sums=('SKIP')

install="${pkgname}.install"

prepare() {
  cd "${srcdir}"
  ar x "Yandex_Music_amd64_${pkgver}.deb"

  # распакуем payload
  tar -xf data.tar.* -C "${srcdir}"

  # исходный deb кладёт всё в /opt/Яндекс Музыка — нормализуем в промежутке:
  _src_opt_dir="${srcdir}/opt/Яндекс Музыка"
  _dst_opt_dir="${srcdir}/opt/yandex-music"
  if [[ -d "${_src_opt_dir}" && ! -e "${_dst_opt_dir}" ]]; then
    mv "${_src_opt_dir}" "${_dst_opt_dir}"
  fi

  # если есть desktop и иконки — оставим для последующей установки
}

package() {
  cd "${srcdir}"

  # создаём директории
  install -d "${pkgdir}/opt" "${pkgdir}/usr/bin" \
             "${pkgdir}/usr/share/applications" \
             "${pkgdir}/usr/share/icons/hicolor"

  # положим приложение в /opt/yandex-music
  cp -a "opt/yandex-music" "${pkgdir}/opt/"

  # бинарь: делаем удобный symlink как в postinst, но без update-alternatives
  ln -s /opt/yandex-music/yandexmusic "${pkgdir}/usr/bin/yandexmusic"

  # desktop-файл: если он есть в deb — перепишем Exec/Icon, иначе сгенерим
  if [[ -f "usr/share/applications/yandexmusic.desktop" ]]; then
    # нормализуем Exec, Icon и StartupWMClass
    sed -E \
      -e 's|^Exec=.*|Exec=yandexmusic %U|' \
      -e 's|^Icon=.*|Icon=yandex-music|' \
      -e 's|^StartupWMClass=.*|StartupWMClass=Yandex Music|' \
      "usr/share/applications/yandexmusic.desktop" \
      > "${pkgdir}/usr/share/applications/yandexmusic.desktop"
    chmod 644 "${pkgdir}/usr/share/applications/yandexmusic.desktop"
  else
    cat > "${pkgdir}/usr/share/applications/yandexmusic.desktop" <<'EOF'
[Desktop Entry]
Name=Яндекс Музыка
Comment=Персональные рекомендации, подборки на любой случай и музыкальные новинки
Exec="/opt/yandex-music/yandexmusic" %U
Terminal=false
Type=Application
Icon=yandex-music
Categories=Audio;
MimeType=x-scheme-handler/yandexmusic;
EOF
  fi

  # иконки (если в deb лежат в стандартных путях)
  if compgen -G "usr/share/icons/hicolor/*/apps/*.png" > /dev/null; then
    # переименуем к единому имени yandex-music.*
    while IFS= read -r -d '' icon; do
      # пример пути: usr/share/icons/hicolor/256x256/apps/whatever.png
      size_dir="$(dirname "$icon")"              # .../apps
      theme_dir="$(dirname "$size_dir")"         # .../256x256
      rel_dir="${theme_dir#usr/}"                # share/icons/hicolor/256x256
      install -Dm644 "$icon" \
        "${pkgdir}/usr/${rel_dir}/apps/yandex-music.${icon##*.}"
    done < <(find usr/share/icons/hicolor -type f -path "*/apps/*" -print0)
  fi

  # лицензия, если была
  if [[ -f "usr/share/doc/yandexmusic/copyright" ]]; then
    install -Dm644 "usr/share/doc/yandexmusic/copyright" \
      "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  fi

  # права на chrome-sandbox: по умолчанию без SUID (Arch с userns обычно ок)
  if [[ -f "${pkgdir}/opt/yandex-music/chrome-sandbox" ]]; then
    chmod 0755 "${pkgdir}/opt/yandex-music/chrome-sandbox"
  fi
}
