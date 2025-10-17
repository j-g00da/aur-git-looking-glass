# Maintainer: everyx <lunt.luo#gmail.com>

pkgname=wepush
pkgdesc="专注批量推送的小而美的工具"
pkgver=5.0.5
pkgrel=1
arch=('any')
url="https://rememberber.github.io/WePush/"
license=('MIT')
depends=("java-runtime")
makedepends=('patch' 'maven' 'java-environment=21')

_appname="WePush"
_distasset="wepush-${pkgver}.tar.gz"
source=("${_distasset}::https://github.com/rememberber/WePush/archive/refs/tags/v${pkgver}.tar.gz"
        "0001-fix-maven-compiler-with-lombok.patch")
sha256sums=('ca8b351cc8967c666098c8a9a12c26efac6c23a6ccdcd2ba90b8eb4106faf70d'
            '27b8a432559ca575f183ecf1b9c2c21a79bb11e156d49f609086c219e1b43b28')

prepare() {
    cd "${srcdir}/${_appname}-${pkgver}"
    for patch in "$srcdir"/*.patch; do
        patch -p1 < "$patch"
    done
}


build() {
    (
        cd "${srcdir}/${_appname}-${pkgver}"
        mvn clean
        mvn package -Dmaven.test.skip=true
    )
}


package() {
    _srcdir="${srcdir}/${_appname}-${pkgver}"
    _distdir="${_srcdir}/target/WePush/WePush.app/Contents/Resources/Java"

    install -Dvm755 "${_distdir}"/*.jar      -t "${pkgdir}/usr/share/java/${pkgname}/"
    install -Dvm644 "${_distdir}"/libs/*.jar -t "${pkgdir}/usr/share/java/${pkgname}/libs/"

    install -Dvm644 /dev/stdin "${pkgdir}/usr/share/applications/$pkgname.desktop" <<END
[Desktop Entry]
Version=1.0
Type=Application
Name=WePush
GenericName=WePush
Comment=WePush
Exec=wepush
Icon=wepush
Terminal=false
StartupNotify=true
Categories=Network;Office;Utility;
END

    install -Dvm755 /dev/stdin "$pkgdir/usr/bin/$pkgname" <<END
#!/bin/sh
exec /usr/bin/java -jar '/usr/share/java/${pkgname}/${_appname}-${pkgver}-runnable.jar' "\$@"
END

    for i in 16 24 32 48 64 128 256 512 1024; do
        install -Dvm644 "${_srcdir}"/src/main/resources/icon/logo-$i.png \
            "$pkgdir/usr/share/icons/hicolor/${i}x${i}/apps/$pkgname.png"
    done
}
