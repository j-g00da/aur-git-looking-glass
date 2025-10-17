# Maintainer: Raphael Nestler <raphael.nestler@gmail.com>
# Contributor: Chloe Colman <chloe.colman7@gmail.com>
# Contributor: Sampson Crowley <sampsonsprojects@gmail.com>
# Contributor: Rhys Kenwell <redrield+aur@gmail.com>
# Github Contributors: https://github.com/SampsonCrowley/arch_packages/contributors.md

pkgname=heroku-cli
pkgver=10.11.0
pkgrel=1
pkgdesc="CLI to manage Heroku apps and services with forced auto-update removed"
arch=('any')
url="https://devcenter.heroku.com/articles/heroku-cli"
license=('custom' 'ISC')
depends=('nodejs>=20.18' 'nodejs<23')
makedepends=('yarn' 'git' 'npm')
optdepends=('git: Deploying to Heroku')
conflicts=('heroku-cli-bin' 'heroku-client-standalone' 'heroku-toolbelt' 'ruby-heroku')
source=("git+https://github.com/heroku/cli.git#commit=v${pkgver}")
sha256sums=('a075e06dc7b029293341de71422e508605415096fb472939b6e6113a328d52d7')
sha512sums=('6cd747a3c58a32a5348f8f4213b295fb27e8410fe7320c69a37441e81a4feef54430ac3b8bafaa15fd938a3e2d84c302c108a2638ce48ff7c633138b225b57c7')
options=('!strip')
provides=('heroku' 'heroku-cli')

prepare() {
  pushd "$srcdir"

    pushd "cli"
      pushd packages/cli
        # remove forced auto-update plugin
        sed -i "/oclif\/plugin-update/d" ./package.json

        # Allow to use nodejs 22
        sed -i 's/"node": "20.x"/"node": ">=20 <23"/g' ./package.json

        # install dependencies, must be done with yarn as of 7.60
        yarn install

        # create base package
        yarn pack --filename "heroku-v$VERSION-linux-x64.tar.xz"
        tar -xzvf "heroku-v$VERSION-linux-x64.tar.xz" -C "$srcdir/"
      popd
    popd

    # Remove any existing package
    rm -rf heroku/
    # final installation
    mv package heroku
    pushd heroku
      yarn --prod
    popd

    # unneeded compilation files
    for file in *; do
      if [[ "$file" = "heroku" ]]; then
        continue
      else
        rm -rf "$file"
      fi
    done
  popd
}

package() {
  install -dm755 "$pkgdir/usr/lib/heroku"
  install -dm755 "$pkgdir/usr/bin"
  install -dm755 "$pkgdir/usr/share/licenses/$pkgname"

  cp -a "$srcdir/heroku" "$pkgdir/usr/lib"

  # completions
  local autocompletedir="$srcdir/heroku/autocomplete-scripts"
  install -Dm644 "$autocompletedir/bash/heroku.bash" "$pkgdir/usr/share/bash-completion/completions/heroku"
  install -Dm644 "$autocompletedir/zsh/_heroku" "$pkgdir/usr/share/zsh/site-functions/_heroku"

  ln -sf "../../../lib/heroku/LICENSE" "$pkgdir/usr/share/licenses/$pkgname"
  ln -sf "../lib/heroku/bin/run" "$pkgdir/usr/bin/heroku"

  # Remove empty directories
  find "${pkgdir}" -type d -empty -delete
}
