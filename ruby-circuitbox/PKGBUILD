# Maintainer: Andrew O'Neill <andrew at haunted dot sh>

_gemname=circuitbox
pkgname=ruby-${_gemname}
pkgver=2.0.0
pkgrel=1
pkgdesc='Ruby circuit breaker gem that protects your application from failures of its service dependencies'
arch=('x86_64')
url="https://github.com/yammer/${_gemname}"
license=('Apache-2.0')
depends=('ruby' 'rubygems')
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('0b06418aa267f67e303567164bd9a8d53cc08e7662e8addba47caf2d3c167e01')

build() {
  cd "${_gemname}-${pkgver}"

  gem build ${_gemname}.gemspec
}

package() {
  cd "${_gemname}-${pkgver}"

  local _gemdir="$(ruby -e'puts Gem.default_dir')"
  gem install --ignore-dependencies --no-user-install -i "${pkgdir}/${_gemdir}" -n "${pkgdir}/usr/bin" ${_gemname}-${pkgver}.gem
  rm "${pkgdir}/${_gemdir}/cache/${_gemname}-${pkgver}.gem"
}
