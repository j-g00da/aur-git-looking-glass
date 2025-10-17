# Maintainer: Andrei A. Bykov <andreiab9019@gmail.com>
pkgname=mkinitcpio-hook-neoshy
pkgver=1.1
pkgrel=1
pkgdesc="Custom mkinitcpio hook to mount container file from block device before running encrypt-hook"
arch=('any')
url="https://github.com/andr31ab/mkinitcpio-hook-neoshy"
license=('MIT')
depends=('mkinitcpio' 'cryptsetup')
source=('hook' 'install' 'README.md' 'README-ru.md' 'CHANGELOG.md')
sha256sums=(
	'61c0a720e08c2d7af3639c691d95e3e3fe607c576346c2aa294c25383e86f121'
	'9031dc358ae5ac9f79117afa9735b4ae318eeeda63c9a8f46b154bdc6c4b369c'
	'18f616624687fcfda5e107481af418ea61ebbf331d1c83a3c317645cf545aaac'
	'18c5effa27400a07e40433d86f3eb0f313f8ad1879f56ca932db04b19d18666a'
	'2753a088d3c423ff550947a060d8c68d4fcb49a7eafc58f05921781a4a00e482')

package() {
    install -Dm755 "$srcdir/hook" "$pkgdir/usr/lib/initcpio/hooks/neoshy"
    install -Dm755 "$srcdir/install" "$pkgdir/usr/lib/initcpio/install/neoshy"
	install -Dm644 "$srcdir/README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
	install -Dm644 "$srcdir/CHANGELOG.md" "$pkgdir/usr/share/doc/$pkgname/CHANGELOG.md"
}
