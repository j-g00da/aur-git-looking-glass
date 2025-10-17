pkgname=init-nitro
pkgver=0.4.1
_nrev="db54b83e790288ec6aa28fbbeda21e6f52c553f4"
_rcrev="e0c4e306e448d2ac7a8a314133995ee37bc48f92a"
_rver=2.2.0
_rpver=20250506
pkgrel=7
pkgdesc='simple init'
arch=('x86_64' 'aarch64')
url='https://github.com/leahneukirchen/nitro'
license=('GPL')
provides=('nitro')
depends=('glibc' 'bash')
conflicts=('svc-manager' 'eudev-nitro')
replaces=('eudev-nitro')
makedepends=()
optdepends=()
groups=()
backup=()
source=(
		"nitro-$pkgver-${_nrev:0:10}.tar.gz::https://github.com/leahneukirchen/nitro/archive/${_nrev}.tar.gz"
		"git+https://gitea.artixlinux.org/artix/runit-rc.git"
		"http://smarden.org/runit/runit-${_rver}.tar.gz"
		"runit-patches-${_rpver}.tar.xz::https://github.com/clan/runit/releases/download/runit-${_rver}-r2/runit-${_rver}-patches-${_rpver}.tar.xz"
        "runit-artix-20210904.tar.gz::https://gitea.artixlinux.org/artix/runit-artix/archive/20210904.tar.gz"
		"etc-nitro.tar.xz"
		"000-services.patch"
		"001-runit-rc.patch"
		"shutdown"
		"nsm"
		"00-init-nitro-remove.hook"
		"99-init-nitro-install.hook"
		"init-nitro-script"
		"nitro-install.hook"
		"nitro-remove.hook"
		"nitro-hook"
		)
sha256sums=('b16f1e65c8e004efa5d4f4406e9e0a4022c86326090b1fba59ccf3beca5a25e2'
            'SKIP'
            '95ef4d2868b978c7179fe47901e5c578e11cf273d292bd6208bd3a7ccb029290'
            'bbd115a9612c5a8df932cd43c406393538389b248ad44f1d9903bc0e2850e173'
            '191f7d0ad00183ab3a8820ca9bf4295de8af6d9bfa06571653e8fd3d8280e63a'
            '3be45d4a6e42ca33bec1ed86dcbfabd70219ab670f3a1dab8bde6cd3ddfdb1d2'
            'fd2659e5f12fd9e108da74fcf128c137892805e085a6d432d088751055ca5f0a'
            'b95c84100bb989a6586da256a40d9e0b8f164c1b535ca0d4e5d3cce537f4c542'
            '08e048595bfac34ef656350c320a93de023e4b0e030a29bddaef3239d9d83d17'
            'eb31194f5f181e58225fb73833a110fafabeb28d7b149cac2cf80242851a284f'
            'c5d1acec2129a16bdc367b8b7aae9645174d940276fb9519832c7098e488c528'
            '50706e557b8f5dcd451f70b7f86c71a2c7cb78efcc7d9726c15f36d6a773f380'
            '979b592f12348e49f7543ad539780af5b6fa7b8d3c3669ca6d683894128be26f'
            'c495dc6223f3bcdc1f9dfb24e64dbf901048eca80fd2219990e086d0e806bba5'
            'e1b28215d691b57b9b75324fb5f4ef62f2b0362412824322dfb9fdcd879aff84'
            'd2e9255b5181d4668c899a90d8cb05730bcb0d98ca05cc1bea785f94df9c6759')
validpgpkeys=()

prepare() {
	local x
	ln -sf nitro-${_nrev} $pkgname-$pkgver
	cd $pkgname-$pkgver
	patch -Np1 -i "$srcdir"/000-services.patch
	cd "$srcdir/runit-rc"
	patch -Np1 -i "$srcdir"/001-runit-rc.patch

	cd "$srcdir/admin/runit-${_rver}/src"
	for x in "${srcdir}"/patches/*; do
		if [ "$VERBOSE" = 1 ]; then
			patch -Np2 -i "$x" 
		else
			patch -Np2 -i "$x" | (grep -e "chpst" -e"utmpset" || true)
		fi
	done
}

build() {
	local icflags="${CFLAGS}"
	cd $pkgname-$pkgver
	[ -n "$DEBUG" ] && CFLAGS="${icflags} -DDEBUG=${DEBUG}"
	make
	CFLAGS="${icflags}"
	cd "${srcdir}/runit-rc"
	make RCRUNDIR=/run/nitro/sv.d
	#from runit pkg
	#cc ${CFLAGS} ${srcdir}/halt.c -o ${srcdir}/halt ${LDFLAGS}

	#cd ${_pkgname}
	#make SERVICEDIR="${_servicedir}"

	cd "${srcdir}/admin/runit-${_rver}"

	CFLAGS="${CFLAGS} -static"
	LDFLAGS="${LDFLAGS} -static"

	if [ "$VERBOSE" = 1 ]; then
		package/compile
	else
		package/compile |& (grep -e "chpst" -e "utmpset" || true)
	fi
}

package() {
	local x
	cd $pkgname-$pkgver
	#binaries
	install -dm755 "${pkgdir}/usr/bin"
	install -Dm755 nitro ${pkgdir}/usr/bin/nitro
	install -Dm755 nitroctl ${pkgdir}/usr/bin/nitroctl
	install -Dm755 ${srcdir}/shutdown ${pkgdir}/usr/bin/shutdown
	install -Dm755 ${srcdir}/init-nitro-script "${pkgdir}/usr/share/libalpm/scripts/init-nitro-script"
	install -Dm644 ${srcdir}/00-init-nitro-remove.hook "${pkgdir}/usr/share/libalpm/hooks/00-init-nitro-remove.hook"
	install -Dm644 ${srcdir}/99-init-nitro-install.hook "${pkgdir}/usr/share/libalpm/hooks/99-init-nitro-install.hook"
	install -Dm755 ${srcdir}/nitro-hook "${pkgdir}/usr/share/libalpm/scripts/nitro-hook"
	install -Dm644 ${srcdir}/nitro-install.hook "${pkgdir}/usr/share/libalpm/hooks/nitro-install.hook"
	install -Dm644 ${srcdir}/nitro-remove.hook "${pkgdir}/usr/share/libalpm/hooks/nitro-remove.hook"
	for x in halt poweroff reboot; do ln -s nitroctl ${pkgdir}/usr/bin/$x;done
	install -Dm755 ${srcdir}/nsm ${pkgdir}/usr/bin/nsm
	install -Dm755 ${srcdir}/admin/runit-${_rver}/command/chpst ${pkgdir}/usr/bin/chpst
	install -Dm755 ${srcdir}/admin/runit-${_rver}/command/utmpset ${pkgdir}/usr/bin/utmpset
	install -Dm755 ${srcdir}/runit-artix/script/zzz ${pkgdir}/usr/bin/zzz

	# man pages
	install -dm755 "${pkgdir}/usr/share/man/man1"
	install -dm755 "${pkgdir}/usr/share/man/man8"
	install -Dm644 ${srcdir}/${pkgname}-${pkgver}/nitroctl.1 "${pkgdir}/usr/share/man/man1/nitroctl.1"
	install -Dm644 ${srcdir}/${pkgname}-${pkgver}/nitro.8 "${pkgdir}/usr/share/man/man8/nitro.8"
	install -Dm644 ${srcdir}/admin/runit-${_rver}/man/chpst.8 "${pkgdir}/usr/share/man/man8/chpst.8"
	install -Dm644 ${srcdir}/admin/runit-${_rver}/man/utmpset.8 "${pkgdir}/usr/share/man/man8/utmpset.8"
	install -Dm644 ${srcdir}/runit-artix/man/zzz.8 "${pkgdir}/usr/share/man/man8/zzz.8"

	cd $srcdir/runit-rc
	make DESTDIR="${pkgdir}" install-rc

	# iputils-specific configuration
	mkdir -p "$pkgdir/usr/lib/sysctl.d"
	echo "net.ipv4.ping_group_range = 0 2147483647" > "$pkgdir/usr/lib/sysctl.d/55-iputils.conf"

	install -dm755  "${pkgdir}/etc"
	cp -pr $srcdir/etc-nitro $pkgdir/etc/nitro
}
