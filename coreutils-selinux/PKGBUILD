# Maintainer: Sébastien "Seblu" Luttringer
# Maintainer: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: judd <jvinet@zeroflux.org>
# SELinux Maintainer: Nicolas Iooss (nicolas <dot> iooss <at> m4x <dot> org)
# SELinux Contributor: Timothée Ravier <tim@siosm.fr>
# SELinux Contributor: Nicky726 (Nicky726 <at> gmail <dot> com)
#
# This PKGBUILD is maintained on https://github.com/archlinuxhardened/selinux.
# If you want to help keep it up to date, please open a Pull Request there.

pkgname=coreutils-selinux
pkgver=9.9
pkgrel=1
pkgdesc='The basic file, shell and text manipulation utilities of the GNU operating system with SELinux support'
arch=('x86_64' 'aarch64')
license=(
  GPL-3.0-or-later
  GFDL-1.3-or-later
)
url='https://www.gnu.org/software/coreutils/'
groups=('selinux')
depends=( 
  acl  
  attr
  glibc
  gmp
  libcap
  libselinux
  openssl
)
makedepends=(
  git
  gperf
  python
  wget
)
conflicts=("${pkgname/-selinux}" "selinux-${pkgname/-selinux}")
provides=("${pkgname/-selinux}=${pkgver}-${pkgrel}"
          "selinux-${pkgname/-selinux}=${pkgver}-${pkgrel}")
source=(
  git+https://git.savannah.gnu.org/git/coreutils.git?signed#tag=v${pkgver}
  git+https://git.savannah.gnu.org/git/gnulib.git
  https://ftp.gnu.org/gnu/${pkgname/-selinux}/${pkgname/-selinux}-${pkgver}.tar.gz{,.sig}
)
validpgpkeys=(
 6C37DC12121A5006BC1DB804DF6FD971306037D9 # Pádraig Brady
)
options=(!lto)
b2sums=('7798d7ba5f9d7f336ad4f9dfd2ae67244e335c898743f0f4fcd735ab6a6799c25bb4fa8ad7bf1fba5ef8a9da832d3d44863bb9fcadcfc2a20ab53c0172b47210'
        'SKIP'
        '31e67d084731be25d01fd7e0d78e774a303dfdd553abb48c6a4fd5515906ee884f00b03f73d6f043dac593e0747a07b4ce3506510ab08422ad4c226c797bd249'
        'SKIP')

prepare() {
  cd "${pkgname/-selinux}"
  # Skip downloading unstable po files in bootstrap scripts to avoid non-deterministic builds
  export SKIP_PO="1"
  # The $SKIP_PO environment variable is only honored by the gnulib submodule if using its "sh" implementation
  export GNULIB_TOOL_IMPL="sh"

  git submodule init
  git config submodule.gnulib.url ../gnulib
  git -c protocol.file.allow=always submodule update

  ./bootstrap

  # apply patch from the source array (should be a pacman feature)
  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    echo "Applying patch $src..."
    patch -Np1 < "../$src"
  done

  # tail -F fails to find out that files are removed, in test VM
  # so disable the tests which verify this
  sed '/^  tests\/tail\/assert\.sh\s/d' -i tests/local.mk
  sed '/^  tests\/tail\/inotify-dir-recreate\.sh\s/d' -i tests/local.mk

  # some tests create directories with long name, which does not work on GitHub Actions
  sed '/^  tests\/du\/long-from-unreadable\.sh\s/d' -i tests/local.mk
  sed '/^  tests\/rm\/deep-2\.sh\s/d' -i tests/local.mk
}

build() {
  cd "${pkgname/-selinux}"
  aclocal -I m4
  autoconf -f
  autoheader -f
  automake -f
  ./configure \
    --prefix=/usr \
    --libexecdir=/usr/lib \
    --with-openssl \
    --enable-no-install-program=hostname,kill,uptime \
    --with-selinux
  make
  
  # Generate coreutils mo files from dist tarball
  cd "${srcdir}/${pkgname/-selinux}-${pkgver}/po"
  for po in *.po; do
    msgfmt "${po}" -o "${po%.po}.mo"
  done
}

check() {
  cd "${pkgname/-selinux}"
  make check
}

package() {
  cd "${pkgname/-selinux}"
  make DESTDIR="${pkgdir}" install

  # Install coreutils mo files from dist tarball
  cd "${srcdir}/${pkgname/-selinux}-${pkgver}/po"
  for mo in *.mo; do
    install -Dm 644 "${mo}" "${pkgdir}/usr/share/locale/${mo%.mo}/LC_MESSAGES/${pkgname/-selinux}.mo"
    install -Dm 644 "${mo}" "${pkgdir}/usr/share/locale/${mo%.mo}/LC_TIME/${pkgname/-selinux}.mo"
  done
}

