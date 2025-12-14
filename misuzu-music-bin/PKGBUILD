# Maintainer: hiruocha <hiruocha at gmail dot com>

pkgname=misuzu-music-bin
pkgver=1.0.17
pkgrel=1
pkgdesc="一个跨平台的本地音乐播放器，支持自动匹配歌词和海报，支持创建歌单，支持日语汉字注音假名。界面仿Apple Music。"
arch=('x86_64')
url="https://github.com/MCDFsteve/misuzumusic"
license=('MIT')
depends=('gtk3' 'mpv' 'zenity')
provides=("${pkgname%-bin}=$pkgver")
conflicts=("${pkgname%-bin}")
options=('!debug')
source=("${pkgname%-bin}-$pkgver.tar.gz::$url/releases/download/v$pkgver/Misuzu-Music-linux-x64-$pkgver.tar.gz"
		"${pkgname%-bin}.png::$url/raw/main/icons/icon.png"
		"${pkgname%-bin}.desktop"
        "$url/raw/main/LICENSE")
sha256sums=('f8dfaa259ee9f48f0d28907de3d8698c9807d87ae462235a0f1caf4330567303'
            'cf54ee24983bfb80f061b00d82cd6f17db1a82da8b1d5f6a7e97115bd7ededc9'
            'd3eb51faad853438e797678b594c3e25b763778b2022847f8862d7bed6e5259a'
            'd674f671ab6551f2d91442d89b0c0f32ff0096893b665d8c467ed6e63539d2d0')

package() {
	install -Dm755 "misuzumusic" "$pkgdir/opt/${pkgname%-bin}/misuzumusic"

    cp -rp "lib" "$pkgdir/opt/${pkgname%-bin}/"
    cp -rp "data" "$pkgdir/opt/${pkgname%-bin}/"

    install -Dm644 "$srcdir/${pkgname%-bin}.desktop" "$pkgdir/usr/share/applications/${pkgname%-bin}.desktop"
    install -Dm644 "$srcdir/${pkgname%-bin}.png" "$pkgdir/usr/share/pixmaps/${pkgname%-bin}.png"
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
