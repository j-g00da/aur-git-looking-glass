# Maintainer: msh356 <msh356@yandex.by>
pkgname=eblande
pkgver=0.5
pkgrel=1
pkgdesc="experimental fan-made desktop environment"
arch=('x86_64')
url="https://t.me/Futanari_OS"
license=('GPL')
depends=('openbox' 'pcmanfm' 'tint2' 'dunst' 'flameshot' 'xdialog' 'bash' 'lxappearance-obconf' 'obconf-qt' 'arandr' 'pavucontrol-qt' 'lxinput' 'picom' 'jgmenu' 'yad')
source=(
    "eblan-autostart"
    "eblande-session"
    "eblande.desktop"
    "eblan-config"
    "eblan-config.desktop"
    "eblan-info"
    "eblan-info.desktop"
    "logo.png"
)
sha256sums=('5b0bc5612b75d7a018744f70149ea61a91bdfb7eb89d3b3a5b583ca53516aeb8'
            'd0990365a6f8a148f2cffa67b097aa07578b9b09df74b7946eb0a77379a6a1f2'
            '727c75f7b8ab80b9b2406f839dfb4ff2a896a9307b794715484a30cc962b4828'
            '626356c999c89bdc3b0c684fb34936dcb7efabbfb1ed14b2572377918d9c9c91'
            'd728726119d6e1f91a4e12e8e7787fc1dc095d2614adf627396f76db4541b705'
            'd4a0edef3bedc7b51754ae8be5a2adeea6a120209bedfe384dc8981988931119'
            '9ac9ae155fd95ce806709521ea005867745dba2904a393ad18ad11ae8c1d1ab5'
            '21077b52a14a39b3ce2cf50f1e79a179d71bcb1bd0c4c4e2b41fd57edcd37513')
package() {
    install -Dm755 "eblan-autostart" "$pkgdir/usr/bin/eblan-autostart"
    install -Dm755 "eblande-session" "$pkgdir/usr/bin/eblande-session"
    install -Dm755 "eblan-config" "$pkgdir/usr/bin/eblan-config"
    install -Dm755 "eblan-info" "$pkgdir/usr/bin/eblan-info"
    install -Dm755 "eblan-config.desktop" "$pkgdir/usr/share/applications/eblan-config.desktop"
    install -Dm755 "eblan-info.desktop" "$pkgdir/usr/share/applications/eblan-info.desktop"
    install -Dm644 "eblande.desktop" "$pkgdir/usr/share/xsessions/eblande.desktop"
    install -Dm644 "logo.png" "$pkgdir/usr/share/eblande/logo.png"
}
