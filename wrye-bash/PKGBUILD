# Maintainer: Infernio <infernio at icloud dot com>

pkgname=wrye-bash
pkgver=314
pkgrel=1
pkgdesc="A swiss army knife for modding Bethesda games"
arch=('any')
license=('GPL-3.0-or-later')
url="https://github.com/wrye-bash/wrye-bash"
depends=('7zip' 'binutils' 'hicolor-icon-theme' 'python' 'python-chardet' 'python-lz4' 'python-reflink' 'python-vdf' 'python-wxpython' 'python-yaml' 'xdg-utils')
optdepends=('python-lxml: FOMOD schema validation'
            'python-pymupdf: PDF support in the doc browser'
            'python-requests: Various Internet-based functionality'
            'python-send2trash: Recycle instead of delete files'
            'python-websocket-client: NexusMods integration (currently unused)')
makedepends=('python-pygit2')
backup=('opt/wrye-bash/bash.ini')
source=("${pkgname}_${pkgver}.tar.gz::https://github.com/wrye-bash/wrye-bash/archive/v${pkgver}.tar.gz"
        "wrye-bash"
        "wrye-bash.desktop"
        "0001-Make-BashBugDump-work-globally.patch")
sha256sums=('663c1d1043483bcfbc0ccfb60b571be7b8bbc6670e93821035ad846cca106f8c'
            'ae3dedbd0dfba70bf159e7420e98e9ccd906b9e7c5a602588869d39849302a93'
            'dd2c34488c4d8f3f43311bdcf9c32d6e7645933eb32eb03f0456adfbed35594f'
            'ef437d64df5d39587280f6c1706cadc9fc20546ff2cc31ddb8424f906bb8fc3c')

prepare() {
    cd "${srcdir}/${pkgname}-${pkgver}"

    # Apply the patchset to make WB (mostly) work as a global installation on Linux
    patch -Np1 -i ../0001-Make-BashBugDump-work-globally.patch

    # Update checking is pointless with pacman available
    sed -i "s/'bash.update_check.enabled': True/'bash.update_check.enabled': False/" Mopy/bash/basher/constants.py

    # Useless binary bloat on Linux
    rm -rf Mopy/bash/compiled

    # Download the taglists if they're missing
    python scripts/update_taglist.py
}

build() {
    cd "${srcdir}/${pkgname}-${pkgver}"

    # Compile the translations
    python scripts/compile_l10n.py

    # Compile all WB source files
    /usr/bin/python -O -m compileall Mopy/bash
}

package() {
    # Install a small script to launch WB
    install -Dm755 wrye-bash "${pkgdir}/usr/bin/wrye-bash"

    # Install a desktop entry, we'll install the logo from the downloaded source
    install -Dm644 wrye-bash.desktop "${pkgdir}/usr/share/applications/wrye-bash.desktop"

    cd "${srcdir}/${pkgname}-${pkgver}"

    # The aforementioned logo
    install -Dm644 Mopy/bash/images/bash.svg "${pkgdir}/usr/share/icons/hicolor/scalable/apps/wrye-bash.svg"

    # Install the data and code to /opt
    mkdir -p "${pkgdir}"/opt/$pkgname
    cp -a "Mopy/Bash Patches" "${pkgdir}"/opt/$pkgname
    cp -a "Mopy/bash" "${pkgdir}"/opt/$pkgname
    cp -a "Mopy/Docs" "${pkgdir}"/opt/$pkgname
    cp -a "Mopy/taglists" "${pkgdir}"/opt/$pkgname
    cp -a "Mopy/templates" "${pkgdir}"/opt/$pkgname
    install -Dm644 "Mopy/Wrye Bash Launcher.pyw" "${pkgdir}"/opt/$pkgname

    # There's no need to package the tests
    rm -r "${pkgdir}"/opt/$pkgname/bash/tests

    # Only the .mo files matter for an end-user build
    rm "${pkgdir}"/opt/$pkgname/bash/l10n/*.po
    rm "${pkgdir}"/opt/$pkgname/bash/l10n/template.pot

    # pacman handles changing config files fine, so skip the _default.ini
    install -Dm644 "Mopy/bash_default.ini" "${pkgdir}"/opt/$pkgname/bash.ini

    # Install the license to /usr
    install -Dm644 LICENSE.md "${pkgdir}"/usr/share/licenses/$pkgname/LICENSE.md
    install -Dm644 Mopy/LICENSE-THIRD-PARTY "${pkgdir}"/usr/share/licenses/$pkgname/LICENSE-THIRD-PARTY
}
