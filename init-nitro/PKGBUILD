pkgname=init-nitro
pkgver=0.5.0
_nrev="8c376d4a5baa7f32999620f9fe3eb51ca8e0dcbc"
_rcrev="e0c4e306e448d2ac7a8a314133995ee37bc48f92a"
_rver=2.2.0
_rpver=20250506
pkgrel=2
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
		"git+https://github.com/replabrobin/init-nitro-rc.git"
		"http://smarden.org/runit/runit-${_rver}.tar.gz"
		"runit-patches-${_rpver}.tar.xz::https://github.com/clan/runit/releases/download/runit-${_rver}-r2/runit-${_rver}-patches-${_rpver}.tar.xz"
		"etc-nitro.tar.xz"
		"000-services.patch"
		"shutdown"
		"nsm"
		"00-init-nitro-remove.hook"
		"99-init-nitro-install.hook"
		"init-nitro-script"
		"nitro-install.hook"
		"nitro-remove.hook"
		"nitro-hook"
		)
sha256sums=('6af4e18010dec7bc074b10025e2e032753b25b3aa1fbcf056ec03fc95a8b4c42'
            'SKIP'
            '95ef4d2868b978c7179fe47901e5c578e11cf273d292bd6208bd3a7ccb029290'
            'bbd115a9612c5a8df932cd43c406393538389b248ad44f1d9903bc0e2850e173'
            'f4367c9b92e715435dd708065aeba1b86f582e1b06decf737e4be25bd69cb0a7'
            '4160f96459cdb454ba5efc21a2949d422cd0ce6df2308c733f50307ecb6e667c'
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
	cd "${srcdir}/init-nitro-rc"
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

	# man pages
	install -dm755 "${pkgdir}/usr/share/man/man1"
	install -dm755 "${pkgdir}/usr/share/man/man8"
	install -Dm644 ${srcdir}/${pkgname}-${pkgver}/nitroctl.1 "${pkgdir}/usr/share/man/man1/nitroctl.1"
	install -Dm644 ${srcdir}/${pkgname}-${pkgver}/nitro.8 "${pkgdir}/usr/share/man/man8/nitro.8"
	install -Dm644 ${srcdir}/admin/runit-${_rver}/man/chpst.8 "${pkgdir}/usr/share/man/man8/chpst.8"
	install -Dm644 ${srcdir}/admin/runit-${_rver}/man/utmpset.8 "${pkgdir}/usr/share/man/man8/utmpset.8"

	cd $srcdir/init-nitro-rc
	make DESTDIR="${pkgdir}" install-rc
	install -Dm644 ${srcdir}/init-nitro-rc/script/zzz.8 "${pkgdir}/usr/share/man/man8/zzz.8"
	install -Dm755 ${srcdir}/init-nitro-rc/script/zzz ${pkgdir}/usr/bin/zzz

	# iputils-specific configuration
	mkdir -p "$pkgdir/usr/lib/sysctl.d"
	echo "net.ipv4.ping_group_range = 0 2147483647" > "$pkgdir/usr/lib/sysctl.d/55-iputils.conf"

	install -dm755  "${pkgdir}/etc"
	cp -pr $srcdir/etc-nitro $pkgdir/etc/nitro
}
