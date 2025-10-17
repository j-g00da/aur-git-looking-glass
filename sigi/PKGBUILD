# Maintainer: J.R. Hill <justin@so.dang.cool>
pkgname="sigi"
pkgver="3.7.1"
pkgrel=2
pkgdesc="Organization CLI for people who hate organization"
arch=('x86_64' 'aarch64')
url="https://github.com/sigi-cli/sigi"
license=('GPL-2.0-only')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::https://crates.io/api/v1/crates/sigi/$pkgver/download")
sha256sums=('9fb629fd2e4644a8e4f173d73c45efad005afe23dd0dbfb0d51dec2f539a28e4')

build() {
	export CARGO_TARGET_DIR=target

	cd "$pkgname-$pkgver"

	cargo build --release --locked
}

check() {
	export CARGO_TARGET_DIR=target

	cd "$pkgname-$pkgver"

	# Tests are skipped until https://github.com/hiljusti/sigi/issues/19
	SKIP_BATS_TESTS=1 cargo test --release --locked
}

package() {
	cd "$pkgname-$pkgver"

	install -Dm755 "target/release/sigi" "$pkgdir/usr/bin/sigi"

	install -Dm644 "sigi.1" "$pkgdir/usr/share/man/man1/sigi.1"
}
