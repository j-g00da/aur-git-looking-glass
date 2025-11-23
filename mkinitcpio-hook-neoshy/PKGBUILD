# Maintainer: Andrei A. Bykov <andreiab9019@gmail.com>
pkgname=mkinitcpio-hook-neoshy
pkgver=1.2
pkgrel=1
pkgdesc="Custom mkinitcpio hook to mount container file from block device before running encrypt-hook"
arch=('any')
url="https://github.com/andr31ab/mkinitcpio-hook-neoshy"
license=('MIT')
depends=('mkinitcpio' 'cryptsetup')
source=('hook' 'install' 'README.md' 'README-ru.md' 'CHANGELOG.md')
sha256sums=(
	'ee2565a266693e3d17daafcb6b9b45af997f892d1d3b1e00cae85c14b00c2d2c'
	'3414397af335d5073e8bc479f1f163e6367aab0f5aad334f799f3c6cf315f0c5'
	'8190fc6022673e0aaffa64ded20a2dd6d35fd44954b20fecc6b8c8c9f8f34f57'
	'6c8bf4b8ad7ec57fa6d867b5bc22fc4af4e57f4a71b64f3f3e1c6d504cc575ba'
	'd49e1e017b864fd67126fb19177586b0fa2ea676a197a25a1196c7b4c17d4c4b')

package() {
    install -Dm755 "$srcdir/hook" "$pkgdir/usr/lib/initcpio/hooks/neoshy"
    install -Dm755 "$srcdir/install" "$pkgdir/usr/lib/initcpio/install/neoshy"
	install -Dm644 "$srcdir/README.md" "$pkgdir/usr/share/doc/$pkgname/README.md"
	install -Dm644 "$srcdir/CHANGELOG.md" "$pkgdir/usr/share/doc/$pkgname/CHANGELOG.md"
}
