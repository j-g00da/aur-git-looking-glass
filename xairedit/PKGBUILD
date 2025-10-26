# Maintainer: Anders Thomsen <mail nospamat andersthomsen nospamdot dk>
# Maintainer: redtide <redtid3@gmail.com>

pkgname=xairedit
pkgver=1.8.1
pkgrel=2
pkgdesc="Remote control program for Behringer X-AIR mixers"
arch=(
  x86_64
  armv7h
)
url="https://www.behringer.com/downloads.html"
license=('custom:MUSIC Group End User License Agreement')
depends=(
  alsa-lib
  freetype2
  curl
  libglvnd
  glibc
  gcc-libs
)
source=('EULA_2012-09-12.pdf'
        'xairedit.desktop')
source_x86_64=("https://cdn.mediavalet.com/aunsw/musictribe/VX4UkGFjQ0a1DH2Q8zg3sg/_KJ6tGIG7kGVqPxP-OsnLQ/Original/X-AIR-Edit_LINUX_$pkgver.tar.gz")
source_armv7h=("https://cdn.mediavalet.com/aunsw/musictribe/VX4UkGFjQ0a1DH2Q8zg3sg/_KJ6tGIG7kGVqPxP-OsnLQ/Original/X-AIR-Edit_RASPI_$pkgver.tar.gz")
sha512sums=('fe39285768937d82f31844b789d1075de8196495727653595e59f4f1b282f6dbe18a8a8bc51b837f284601dc37c52211d3d494a8636512f5398da31ff3d30284'
            '3633f4225036a4e6499d48a350d852028c955a4cf749a95a876022ff64f6d12d801814e6953c8a0c1f428d2f63a2e99ff8296130bafcd6aedfe0126160c649a4')
sha512sums_x86_64=('cd5f2b3a6bb25416724a4a2418d0407ce7914115ebcf10c218e66bc7560f584d3e467d1bf1214a4fb5ac2fb301f8cf3ce7db638fde4a675255266d73798f508e')
sha512sums_armv7h=('cd5f2b3a6bb25416724a4a2418d0407ce7914115ebcf10c218e66bc7560f584d3e467d1bf1214a4fb5ac2fb301f8cf3ce7db638fde4a675255266d73798f508e')
b2sums=('f3af5fcb0044782d51ef976375b6184d781bab5110fb2184ac40443df7b21fdfc12ffa534448bb0aa41df8210c5e63a7d2995ee54279c2ec0824de5eb83aae64'
        '1c1d89adf7e57cb49c2e87de2a3c90ddeedf066b66a3b74e72ae6bac64da2bb3daa92788ec2577050e65dda70a8b4985cc4dfb23ebba74ca7ebbbc848b5d3ba5')
b2sums_x86_64=('0065d4a6306fde3a854bb213ce427eae035dd89b23cb065ba0e1f801feaf8fc952c048cc0b4823e4604787a59381fe9d5d4b7f89404f7bd2599e92975fd9a138')
b2sums_armv7h=('0065d4a6306fde3a854bb213ce427eae035dd89b23cb065ba0e1f801feaf8fc952c048cc0b4823e4604787a59381fe9d5d4b7f89404f7bd2599e92975fd9a138')

package()
{
    cd "$srcdir"
    install -Dm755 X-AIR-Edit "$pkgdir"/usr/bin/$pkgname
    install -Dm644 EULA_2012-09-12.pdf "$pkgdir"/usr/share/licenses/$pkgname/license.pdf
    install -Dm644 xairedit.desktop -t "$pkgdir"/usr/share/applications
}
