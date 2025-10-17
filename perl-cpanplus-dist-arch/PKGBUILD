# Maintainer: Morgenstern <charles [at] charlesbwise [dot] com>
# Contributor: Florian Pritz <bluewind@xinu.at>
# Generator  : CPANPLUS::Dist::Arch 1.32

pkgname='perl-cpanplus-dist-arch'
pkgver='1.32'
pkgrel='13'
pkgdesc="CPANPLUS backend for building Archlinux pacman packages"
arch=('any')
license=("Artistic-2.0"
         "GPL-1.0-only")
options=('!emptydirs')
depends=('perl-cpanplus>=0' 'perl-pod-parser>=0')
makedepends=()
url='https://metacpan.org/release/CPANPLUS-Dist-Arch'
source=('http://search.cpan.org/CPAN/authors/id/J/JN/JNBEK/CPANPLUS-Dist-Arch-1.32.tar.gz')
md5sums=('673be0f0651e975faf4aa59536361d60')
sha512sums=('92aa6214c56b73c5ce48998a9cc86d619ac3e8c01c1cd3445a99fc9dbc4740923f0cc7708f7270dbc1e930cc783366f98833a8ae58a62f225b614d626c79665d')
_distdir="CPANPLUS-Dist-Arch-1.32"

build() {
  ( export PERL_MM_USE_DEFAULT=1 PERL5LIB=""                 \
      PERL_AUTOINSTALL=--skipdeps                            \
      PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'"     \
      PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
      MODULEBUILDRC=/dev/null

    cd "$srcdir/$_distdir"
    /usr/bin/perl Makefile.PL
    make
  )
}

check() {
  cd "$srcdir/$_distdir"
  ( export PERL_MM_USE_DEFAULT=1 PERL5LIB=""
    make test
  )
}

package() {
  cd "$srcdir/$_distdir"
  make install
  find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
}

# Local Variables:
# mode: shell-script
# sh-basic-offset: 2
# End:
# vim:set ts=2 sw=2 et:
