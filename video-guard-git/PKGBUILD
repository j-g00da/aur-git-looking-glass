# Maintainer: littleblack111 <littleblack11111@gmail.com>
pkgname=video-guard-git
_pkgname=video-guard
pkgver=r11.06bcc88
pkgrel=1
pkgdesc="Helper that guards and requests user confirmation for /dev/video* access"
arch=('any')
url="https://github.com/littleblack111/video-guard"
license=('GPL-3.0-or-later')
depends=('lsof' 'bash' 'systemd' 'libnotify' 'coreutils' 'gawk')
optdepends=('hyprland-qtutils: to use default dialog')
makedepends=('git' 'clang' 'bpf' 'gcc' 'libbpf')
source=("git+https://github.com/littleblack111/video-guard.git")
sha256sums=('SKIP')

pkgver() {
	cd "$_pkgname"
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

build() {
	cd "$_pkgname"
	# helpers
	clang -O2 -g \
		-I/usr/include \
		-target bpf \
		-c helper/kernel.c -o kernel.bpf.o
	bpftool gen skeleton kernel.bpf.o >kernel.skel.h
	g++ -O2 -std=c++26 \
		helper/user.cpp \
		-I. -I/usr/include/bpf \
		-lbpf -lelf -lz -pthread \
		-o video-guard-helper
}

package() {
	cd "$_pkgname"
	install -Dm755 videoGuard.sh "$pkgdir/usr/bin/video-guard"
	install -Dm4755 -o root -g root video-guard-helper "$pkgdir/usr/bin/video-guard-helper"
	install -Dm644 video-guard.service "$pkgdir/etc/systemd/system/video-guard.service"
}

post_install() {
	echo "To enable the service, run systemctl --user enable --now shut-userspace.service"
	echo "Important: for this to work, you need special permissions for lsof(/sys/kernel/debug/tracing)"
	echo "You can set it up by running: sudo setcap cap_sys_admin+ep /usr/bin/lsof"
}
