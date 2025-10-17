# Maintainer: AlphaLynx <alphalynx at alphalynx dot dev>

pkgname=kiro-bin
_name="${pkgname%-bin}"
pkgver=0.4.0
pkgrel=1
epoch=1
pkgdesc='The AI IDE for prototype to production'
arch=('x86_64')
url='https://kiro.dev/'
# By downloading and using Kiro, you agree to the following:
#   AWS Customer Agreement: https://aws.amazon.com/agreement/
#   AWS Intellectual Property License: https://aws.amazon.com/legal/aws-ip-license-terms/
#   Service Terms: https://aws.amazon.com/service-terms/
#   Privacy Notice: https://aws.amazon.com/privacy/
license=('LicenseRef-AWS-IPL')
makedepends=('openssl')
depends=(
    'alsa-lib'
    'at-spi2-core'
    'bash'
    'cairo'
    'dbus'
    'expat'
    'gcc-libs'
    'glib2'
    'glibc'
    'gtk3'
    'libcups'
    'libx11'
    'libxcb'
    'libxcomposite'
    'libxdamage'
    'libxext'
    'libxfixes'
    'libxkbcommon'
    'libxkbfile'
    'libxrandr'
    'mesa'
    'nodejs'
    'nspr'
    'nss'
    'pango'
    'perl'
    'python'
    'systemd-libs'
)
provides=("$_name")
conflicts=("$_name")
options=('!debug' '!strip')
_timestamp=202510142329
_baseurl=https://prod.download.desktop.kiro.dev/releases/$_timestamp--distro-linux-x64-tar-gz
source=(
    "$_name-$_timestamp.tar.gz::$_baseurl/$_timestamp-distro-linux-x64.tar.gz"
    "$_name-certificate.pem::$_baseurl/certificate.pem"
    "$_name-$_timestamp-signature.bin::$_baseurl/signature.bin"
    "$_name.desktop"
    "$_name-url-handler.desktop"
    "$_name-workspace.xml"
)
b2sums=('0b66a679210b0784e383e302d5b0ca17539c5099af50f8e916223258f1c6b003474d315894faba7ee56809bd03f6191f5c354e218293e9f29d871e7d36d09cb6'
        '09676f21f9b2821f7fb789fde98f1825f53d1df64ab74932ec2117f6cf06985bc5795ea7a016d90e9318035b2dd7c2f9706dccf44eb4cd092e4268a5f4760a26'
        '725298776d93c92d86160b46e6b1bd927d4e168cfcf8da09ce2406d49c3e298abcf3542b0bf87f3aeb42a8f7790f427d7eeb4578d9480152c5c45f1a6a491b20'
        '9abc47ecba54f83a1e318d12ef7e4262ce1aeef6933d95eda069e60fcec0c880802841aff268fe56e47a6a69253b409d7079687d2d8b7293f62e0034c3e3a9a7'
        'fd694d647fe06c439026f1a570fba288fb51bf41fe76de60af1e911255e4692b5a3cae1a8c279ed77a4990618b957591b79b6f152728374af97bea1189691014'
        'bf76f34c64e272831da98a3642f827b159582fafb3918db9f7334ed7ed9eace747148d6f0f863d2a5f1e751b7d43f109e35a8ac7ee1985c09d7ea90b73a40455')

verify() {
    openssl x509 -pubkey -noout -in $_name-certificate.pem > kiro-pubkey.pem
    openssl dgst -sha256 -verify kiro-pubkey.pem -signature $_name-$_timestamp-signature.bin \
        $_name-$_timestamp.tar.gz
}

package() {
    mkdir -p "$pkgdir/opt/Kiro"
    cp -r Kiro/* "$pkgdir/opt/Kiro"

    mkdir -p "$pkgdir/usr/bin"
    ln -s /opt/Kiro/bin/$_name "$pkgdir/usr/bin/$_name"

    mkdir -p "$pkgdir/usr/share/licenses/$pkgname"
    ln -s /opt/Kiro/resources/app/LICENSE.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE.txt"

    mkdir -p "$pkgdir/usr/share/pixmaps"
    ln -s /opt/Kiro/resources/app/resources/linux/code.png "$pkgdir/usr/share/pixmaps/$_name.png"

    mkdir -p "$pkgdir/usr/share/bash-completion/completions"
    mkdir -p "$pkgdir/usr/share/zsh/site-functions"

    ln -s /opt/Kiro/resources/completions/bash/$_name \
        "$pkgdir/usr/share/bash-completion/completions/$_name"
    ln -s /opt/Kiro/resources/completions/zsh/_$_name \
        "$pkgdir/usr/share/zsh/site-functions/_$_name"

    install -Dm644 $_name.desktop "$pkgdir/usr/share/applications/$_name.desktop"
    install -Dm644 $_name-url-handler.desktop \
        "$pkgdir/usr/share/applications/$_name-url-handler.desktop"
    install -Dm644 $_name-workspace.xml "$pkgdir/usr/share/mime/packages/$_name-workspace.xml"
}
