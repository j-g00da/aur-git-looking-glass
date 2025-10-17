# Maintainer: Breno Ramalho Lemes <breno@br-lemes.net>
pkgname=mysqldump57-bin
pkgver=5.7.44
pkgrel=1
pkgdesc="mysqldump from MySQL 5.7 for compatibility with older servers"
arch=('x86_64')
url="https://dev.mysql.com/"
license=('GPL')
depends=('glibc' 'gcc-libs')
source=("https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-${pkgver}-linux-glibc2.12-x86_64.tar.gz")
sha256sums=('798ff0a14cdc1ab259f8a3b6a7f683403e9bbaa85957d82e5370f82b27ba6805')
noextract=("${source[@]##*/}")

prepare() {
    bsdtar -x --strip-components=2 -C "${srcdir}" -f \
        "mysql-${pkgver}-linux-glibc2.12-x86_64.tar.gz" \
        "mysql-${pkgver}-linux-glibc2.12-x86_64/bin/mysqldump"
}

package() {
    install -Dm755 "${srcdir}/mysqldump" "${pkgdir}/usr/local/bin/mysqldump"
}
