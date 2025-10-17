# Maintainer: Andrew O'Neill <andrew at haunted dot sh>

_gemname=oci
pkgname=ruby-${_gemname}
pkgver=2.22.0
pkgrel=1
pkgdesc='Ruby SDK for Oracle Cloud Infrastructure'
arch=('x86_64')
url='https://github.com/oracle/oci-ruby-sdk'
license=('Apache-2.0 OR UPL-1.0')
depends=('ruby' 'ruby-circuitbox' 'ruby-event_stream_parser' 'ruby-inifile' 'ruby-jwt')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz")
sha256sums=('a2eadab38a6c0fd38129b11f8ff9ee2d21a06bc9e15f3a3f1f31e371ba125343')

build() {
  cd "${_gemname}-ruby-sdk-${pkgver}"

  gem build ${_gemname}.gemspec
}

package() {
  cd "${_gemname}-ruby-sdk-${pkgver}"

  local _gemdir="$(ruby -e'puts Gem.default_dir')"
  gem install --ignore-dependencies -N --no-user-install -i "${pkgdir}/${_gemdir}" -n "${pkgdir}/usr/bin" ${_gemname}-${pkgver}.gem
  rm "${pkgdir}/${_gemdir}/cache/${_gemname}-${pkgver}.gem"
  install -Dm644 LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
