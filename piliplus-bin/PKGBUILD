# Maintainer: Ethan <yeah_yaojiu@163.com>

pkgname=piliplus-bin
pkgver=1.1.4.14
_version=1.1.4+4282
pkgrel=1
url="https://github.com/bggRGjQaUbCoE/PiliPlus"
pkgdesc="A Bilibili third-party client built with Flutter. | 使用Flutter开发的BiliBili第三方客户端"
arch=('x86_64')
license=('GPL-3.0')
depends=('gtk3' 'mpv' 'libayatana-appindicator')
source=("${url}/releases/download/${pkgver}/PiliPlus_linux_${_version}_amd64.tar.gz")
options=(!debug)

sha256sums=('d2f87d37d419b11f1bbb0cfda3e5a296ca0953059f0621acdafb94d919f4418a')

package() {

  install -d "$pkgdir/opt/$pkgname"
  
  cp "$srcdir/piliplus" "$pkgdir/opt/$pkgname/"
  cp -r "$srcdir/lib" "$pkgdir/opt/$pkgname/"
  cp -r "$srcdir/data" "$pkgdir/opt/$pkgname/"


 install -Dm644 "$srcdir/data/flutter_assets/assets/images/logo/logo.png" \
    "$pkgdir/usr/share/icons/hicolor/256x256/apps/$pkgname.png"

  install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/$pkgname.desktop" <<EOF
[Desktop Entry]
Name=PiliPlus
Comment=A Bilibili third-party client built with Flutter.
Exec=piliplus
Icon=$pkgname
Terminal=false
Type=Application
Categories=Utility;
EOF

  install -d "$pkgdir/usr/bin"
  ln -s "/opt/$pkgname/piliplus" "$pkgdir/usr/bin/piliplus"
}
