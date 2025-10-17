# Maintainer: AlphaJack <alphajack at tuta dot io>

pkgname="teams-for-linux-bin"
pkgver=2.2.1
pkgrel=1
pkgdesc="Unofficial Microsoft Teams for Linux client (binary version)"
url="https://github.com/IsmaelMartinez/teams-for-linux"
license=("GPL3")
arch=("x86_64" "aarch64" "armv7h")
provides=("teams-for-linux")
conflicts=("teams-for-linux"
           "teams-for-linux-appimage"
           "teams-for-linux-git"
           "teams-for-linux-wbundled-electron"
          )
depends=("gtk3" "libxss" "nss")
source_x86_64=("$url/releases/download/v$pkgver/teams-for-linux_${pkgver}_amd64.deb")
source_aarch64=("$url/releases/download/v$pkgver/teams-for-linux_${pkgver}_arm64.deb")
source_armv7h=("$url/releases/download/v$pkgver/teams-for-linux_${pkgver}_armv7l.deb")
b2sums_x86_64=('0ce655a4eb4cb0de720d87f2e9b46a65efa84ec5a3fd6055630036c80d1800036d339cf7b0703ef55e4666fcd555c316aa26e757c6d8ea82805c468a95b1634f')
b2sums_aarch64=('fb8a3bfeb698530d5fb79bb4637a1c71f2747f2e748632def3dc3c70ad1cf3f953467dbfd009e5d1350720ce73d9134dbf8661c113f6b810dc3b3fb5247c9b6a')
b2sums_armv7h=('60f22de1cccefb75905bab3d5c8ad4c0641edee36b436ba0e90ff24b0d9bec8cdbe447959094bc5e3a5cd54fb84cc542bceebf509cfb468b73f5949c973b0d73')
options=("!strip")

prepare(){
 tar -xf "data.tar.xz"
}

package(){
 cp -r "opt" "$pkgdir"
 cp -r "usr" "$pkgdir"
}
