pkgname=atproto-pds
pkgver=0.4.193
pkgrel=1
pkgdesc='AT Protocol PDS (Personal Data Server)'
url='https://github.com/bluesky-social/pds'
license=(MIT Apache-2.0)
arch=(x86_64 aarch64)
depends=(nodejs)
makedepends=(npm)
source=(
  "git+https://github.com/bluesky-social/pds.git#tag=v$pkgver"
  pds.sh
  pdsadmin.sh
  pds.service
  pds.sysusers
  pds.tmpfiles
  pds.env
)
md5sums=(
  SKIP
  a8c172c210f7284ed51b5784abdeebdd
  6e6a5977c033335fc6b9dd5dfb755530
  f95b4112b45a5fbaeb7e2fcd3a9be930
  1428828b56dbcb0e7ffaf91b6ce13657
  255bc1f00bfd37afe0c683a46028f049
  44a260c5bc36e339ed66f026238520ad
)
install="$pkgname.install"
backup=(etc/pds.env)

build() {
  cd "$srcdir/pds/service"
  # Patch newer better-sqlite3 for Node.js 24.x support
  head -n-1 package.json >package.json.tmp
  cat >>package.json.tmp <<EOF
  ,"overrides": {
    "@atproto/pds": {
      "better-sqlite3": "^12.0.0"
    }
  }
EOF
  tail -n1 package.json >>package.json.tmp
  mv package.json.tmp package.json
  # Install library files
  npm install
}

package() {
  mkdir -p "$pkgdir"/{etc,usr/{bin,lib/atproto-pds{,admin}}}
  # Add library files
  install -Dm 0644 "$srcdir/pds/service/index.js" "$pkgdir/usr/lib/atproto-pds/"
  cp -ar "$srcdir/pds/service/node_modules" "$pkgdir/usr/lib/atproto-pds/"
  # Add entrypoint script for pds application
  install -Dm 0755 "$srcdir/pds.sh" "$pkgdir/usr/bin/pds"
  # Add pdsadmin scripts
  for script in "$srcdir/pds/pdsadmin"/*.sh; do
    target="$pkgdir/usr/lib/atproto-pdsadmin/$(basename "$script")"
    install -Dm 0755 "$script" "$target"
    sed -i 's!/pds/pds.env!/etc/pds.env!g' "$target"
  done
  # Add custom script dispatcher
  install -Dm 0755 "$srcdir/pdsadmin.sh" "$pkgdir/usr/bin/pdsadmin"
  # Add user configuration
  install -Dm 0644 pds.service "${pkgdir}/usr/lib/systemd/system/pds.service"
  install -Dm 0644 pds.sysusers "${pkgdir}/usr/lib/sysusers.d/pds.conf"
  install -Dm 0644 pds.tmpfiles "${pkgdir}/usr/lib/tmpfiles.d/pds.conf"
  # Add default configuration
  install -Dm 0640 pds.env "${pkgdir}/etc/pds.env"
}
