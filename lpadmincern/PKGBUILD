# Maintainer: Wainer Vandelli <wainer dot vandelli at gmail dot com>
# Contributor : Kevin Franz Stehle <kevin dot franz dot stehle at cern dot ch>
pkgname=lpadmincern
pkgver=1.4.9
pkgrel=2
pkgdesc="CERN LDAP printer database client. Note: CERN IT does not provide official support for Arch Linux. Use at your own risk."
url="https://linux.web.cern.ch/docs/printing/"
arch=('any')
license=('GPL')
depends=('cups' 'python' 'python-ldap')
optdepends=()
makedepends=('gzip' 'tar')
conflicts=()
replaces=()
backup=()
source=("https://linuxsoft.cern.ch/cern/alma/9/CERN/x86_64/Packages/l/lpadmincern-${pkgver}-1.al9.cern.noarch.rpm")
md5sums=('70dd526357fcf58605736b7028cc124d')

package() {
  msg2 "Creating directories"
  mkdir -p "${pkgdir}"/usr/bin
  mkdir -p "${pkgdir}"/usr/share/"${pkgname}"/ppds/
  mkdir -p "${pkgdir}"/usr/share/man/man1
  mkdir -p "${pkgdir}"/usr/share/man/man8
  mkdir -p "${pkgdir}"/usr/share/doc/"${pkgname}"
  mkdir -p "${pkgdir}"/usr/lib/systemd/system
  mkdir -p "${pkgdir}"/etc/sysconfig

  msg2 "Installing scripts"
  install -m755 usr/sbin/"${pkgname}" "${pkgdir}"/usr/bin/"${pkgname}"
  install -m644 usr/share/"${pkgname}"/ppds/* "${pkgdir}"/usr/share/"${pkgname}"/ppds/

  install -m644 usr/lib/systemd/system/* "${pkgdir}"/usr/lib/systemd/system/
  install -m644 etc/sysconfig/lpadmincern "${pkgdir}"/etc/sysconfig/

  install -m755 usr/bin/lpq.cern "${pkgdir}"/usr/bin/lpq.cern
  install -m755 usr/bin/lprm.cern "${pkgdir}"/usr/bin/lprm.cern

  msg2 "Creating symlinks"
  pushd "${pkgdir}"/usr/bin > /dev/null
  ln -sf cancel cancel.cern
  ln -sf lp lp.cern
  ln -sf lpr lpr.cern
  ln -sf lpstat lpstat.cern
  ln -sf lpc lpc.cern
  popd > /dev/null

  msg2 "Installing manpages"  
  install -m644 usr/share/man/man1/"${pkgname}".1.gz "${pkgdir}"/usr/share/man/man1/"${pkgname}".1.gz
  install -m644 usr/share/man/man1/cancel-cern.1.gz "${pkgdir}"/usr/share/man/man1/cancel-cern.1.gz
  install -m644 usr/share/man/man1/lp-cern.1.gz "${pkgdir}"/usr/share/man/man1/lp-cern.1.gz
  install -m644 usr/share/man/man1/lpq-cern.1.gz "${pkgdir}"/usr/share/man/man1/lpq-cern.1.gz
  install -m644 usr/share/man/man1/lpr-cern.1.gz "${pkgdir}"/usr/share/man/man1/lpr-cern.1.gz
  install -m644 usr/share/man/man1/lprm-cern.1.gz "${pkgdir}"/usr/share/man/man1/lprm-cern.1.gz
  install -m644 usr/share/man/man1/lpstat-cern.1.gz "${pkgdir}"/usr/share/man/man1/lpstat-cern.1.gz
  install -m644 usr/share/man/man8/lpc-cern.8.gz "${pkgdir}"/usr/share/man/man8/lpc-cern.8.gz
  
  msg2 "Installing docs"
  install -m644 usr/share/doc/"${pkgname}"/README "${pkgdir}"/usr/share/doc/"${pkgname}"/README 
}
