# Maintainer: Lex Black <autumn-wind@web.de>

pkgname=prosody-mod-http-libjs
pkgver=2025.04.09
pkgrel=1
_commit="0bd1804baae7"
pkgdesc="Serve common Javascript libraries"
arch=('any')
url="https://modules.prosody.im/mod_http_libjs.html"
license=('MIT')
depends=('prosody')
makedepends=('mercurial')
optdepends=("jquery: for the default html templates"
            "bootstrap: for the default html templates")
source=("hg+https://hg.prosody.im/prosody-modules/"#revision=$_commit)
sha1sums=('373244c05105fb61c51d40771e6077afabb448e3')


package() {
  cd "${srcdir}/prosody-modules/mod_http_libjs"
  find . -type f -name '*.lua' -exec install -Dm 644 '{}' "${pkgdir}/usr/lib/prosody/modules/{}" \;
  find . -type f ! -name '*.lua' -exec install -Dm 644 '{}' "${pkgdir}/usr/share/doc/${pkgname}/{}" \;
}
