# Maintainer: fk29g <fk29g.uphill912@slmails.com>
_projectname=flashlight
pkgname=$_projectname-bin
pkgver=0.18.0
pkgrel=1
arch=("x86_64")
pkgdesc="Lighthouse for Mobile - audits your Android app and gives a performance score"
url="https://github.com/bamlab/flashlight/"
license=("MIT")
options=("!strip")
conflicts=("$_projectname")
source=("$_projectname-$pkgver.zip::$url/releases/download/v$pkgver/${_projectname}-linux.zip"
        "$_projectname-LICENSE::https://raw.githubusercontent.com/bamlab/$_projectname/refs/heads/main/LICENSE")
b2sums=("65dab92a466d5bcb129fbb7a8ffd57cc3b3430f5bf4916f23d227002bd953ac60c9bbfa524c7ef291c12ec123429b6b51c2219a94a2b56daa14978350cf36196"
        "f259bc34c49eebfbf67f310a5589bb84c09c7476795e66c9bc650627492f92915f7e949e10c842077349b33f7a2238fb15a50322ce539633d4f081505e69ff43")

package() {
    install -Dm 0755 flashlight-linux "${pkgdir}/usr/bin/flashlight"
    install -Dm 0644 $_projectname-LICENSE "${pkgdir}/usr/share/licenses/${_projectname}/LICENSE"
}
