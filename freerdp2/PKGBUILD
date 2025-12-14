# Maintainer: David Runge <dvzrv@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Stijn Segers <francesco dot borromini at gmail dot com>

_name=FreeRDP
pkgname=freerdp2
pkgver=2.11.7
pkgrel=5
pkgdesc="Free implementation of the Remote Desktop Protocol (RDP)"
arch=(x86_64)
url="https://www.freerdp.com/"
license=(Apache-2.0)
depends=(
  glibc
  libcups
  libx11
  libxcursor
  libxext
  libxdamage
  libxfixes
  libxkbcommon
  libxi
  libxinerama
  libxkbfile
  libxrandr
  libxrender
  libxtst
  pcsclite
  wayland
)
makedepends=(
  alsa-lib
  cmake
  docbook-xsl
  ffmpeg
  icu
  krb5
  libjpeg-turbo
  libpulse
  libusb
  openssl
  pam
  systemd
  xmlto
  xorgproto
)
provides=(
  libfreerdp2.so
  libfreerdp-client2.so
  libfreerdp-server2
  libfreerdp-shadow2.so
  libfreerdp-shadow-subsystem2.so
  libwinpr2.so
  libwinpr-tools2.so
  libuwac0.so
)
source=(
  https://github.com/${_name,,}/${_name,,}/archive/$pkgver/${_name,,}-$pkgver.tar.gz
  d0c5b1ae.patch
  1ef7b9e3.patch
  ffmpeg-8.patch
)
sha512sums=('3a308346b2825a06f60e4c3eaf335c151351ecc6e4b990d63d3ef4da1bc6e6de3fb77aefd041bad4bcb40b9269d9ea8d627ac24786c927e4eaaaac2d4ae4b4b9'
            'f7d231fa8aaf08a20b4bbdb153219e94ba6518eee3238f6c26f2c928cd33ad6c975d2c62acb706ad5b0352889b5a9849cffb6e03b2a2e760accd31c492f6a0a9'
            'f5843f8daaa8225534b05dca3d6c1d26a25174d773c81495c73924298312d0c4aee39165a4fe0b4ba38676d40a6779b33443a761f094dd4e16c1303dec026841'
            '7d9051fd984883dd1ce298274135691959670b580569de192818f5ac73ce00847dfa1ae83b72808b8cdc5a33cc9231afde932d4075e337242960d9269de4fd62')
b2sums=('9c401d2e158447cb515f0412142e58394bdeb8df878ef2ac1bd491363c7e2ecbe57f6010ff157cfba72f257fd61a9551f767d19ad0a91e7e1bc0f0ab12e28c54'
        '99f60d738ebb594b3f48895bac567c5a4ba8f1e6ceb2a21d421c842d08f267b49f870c70ca7862fea3340ab247bf232dffd7f4b83ebb9bded2bdec9207cc1d1b'
        'a0157137a52f3f4817908d86b0a3ec575a7307ec05d3f2388a49fe40e9c40ea23aec4fdc6f926ac5b5c443d6d4063e2b35ad1e386577dcf5d5b208fc791a2605'
        '4fe79a1146c39c38496db3f5cd4a1c4c1300cba72f739845b28fc9d38b547607073b923aad404aa6f14431a3fb204634cf4c503c14355a42d995f3d61d7de227')

prepare() {
  cd $_name-$pkgver
  # Fix build with ffmpeg 7
  patch -p1 -i ../d0c5b1ae.patch
  patch -p1 -i ../1ef7b9e3.patch
  # Fix build with ffmpeg 8
  patch -p1 -i ../ffmpeg-8.patch
}

build() {
  # gcc14 buildfix
  export CFLAGS+=" -Wno-incompatible-pointer-types -Wno-int-conversion"
  export CXXFLAGS+=" -Wno-incompatible-pointer-types -Wno-int-conversion"

  local cmake_options=(
    -B build
    -D CHANNEL_URBDRC_CLIENT=ON
    -D CMAKE_INSTALL_PREFIX=/usr
    -D CMAKE_INSTALL_LIBDIR=lib
    -D CMAKE_BUILD_TYPE=None
    -D CMAKE_SKIP_INSTALL_RPATH=ON
    -D PROXY_PLUGINDIR=/usr/lib/freerdp2/server/proxy/plugins
    -D WITH_CHANNELS=ON
    -D WITH_CLIENT_CHANNELS=ON
    -D WITH_CUPS=ON
    -D WITH_DSP_FFMPEG=ON
    -D WITH_FFMPEG=ON
    -D WITH_ICU=ON
    -D WITH_JPEG=ON
    -D WITH_PCSC=ON
    -D WITH_PULSE=ON
    -D WITH_SERVER=ON
    -D WITH_SERVER_CHANNELS=ON
    -D WITH_SWSCALE=ON
    -S $_name-$pkgver
    -W no-dev
  )

  # Fix build with CMake 4.0; proper fix rejected upstream
  # (https://github.com/FreeRDP/FreeRDP/issues/11707).
  cmake_options+=(-D CMAKE_POLICY_VERSION_MINIMUM=3.5)

  cmake "${cmake_options[@]}"
  cmake --build build --verbose
}

check() {
  ctest --test-dir build --output-on-failure
}

package() {
  depends+=(
    alsa-lib libasound.so
    ffmpeg libavcodec.so libavutil.so libswresample.so libswscale.so
    icu libicuuc.so
    libjpeg-turbo libjpeg.so
    libpulse libpulse.so
    libusb libusb-1.0.so
    openssl libcrypto.so libssl.so
    pam libpam.so
    systemd-libs libsystemd.so
  )

  DESTDIR="$pkgdir" cmake --install build
  install -vDm 644 $_name-$pkgver/{ChangeLog,README.md} -t "$pkgdir/usr/share/doc/$pkgname/"
}
