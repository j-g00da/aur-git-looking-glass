# Maintainer: Lex Black <autumn-wind@web.de>

pkgname=prosody-mod-register-apps
pkgver=2025.04.09
pkgrel=1
_commit="8c98b1dd1ad3"
pkgdesc="Manage list of compatible client apps"
arch=('any')
url="https://modules.prosody.im/mod_register_apps.html"
license=('MIT')
depends=('prosody')
makedepends=('mercurial')
source=("hg+https://hg.prosody.im/prosody-modules/"#revision=$_commit)
sha1sums=('0ce53479874750f84f16c03461b982eb2abe1624')


package() {
  cd "prosody-modules/mod_register_apps"
  find . -type f -name '*.lua' -exec install -Dm 644 '{}' "${pkgdir}/usr/lib/prosody/modules/{}" \;
  install -Dm644 assets/logos/* -t "${pkgdir}/usr/lib/prosody/modules/assets/logos/"
  find . -type f ! -name '*.lua' -exec install -Dm 644 '{}' "${pkgdir}/usr/share/doc/${pkgname}/{}" \;
  rm -r "${pkgdir}/usr/share/doc/${pkgname}/assets"
}
