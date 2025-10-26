# Maintainer : Daniel Bermond <dbermond@archlinux.org>
# Contributor: Rainmaker <rainmaker52@gmail.com>
# Contributor: gary9872	<garysBoXatgeemale.com>
# Contributor: khomutsky <bogdan@khomutsky.com>
# Contributor: M0Rf30

pkgbase=virtualbox-bin
pkgname=(
    'virtualbox-bin'
    'virtualbox-bin-guest-iso'
    'virtualbox-bin-sdk')
pkgver=7.2.4
_build=170995
_rev=110274
pkgrel=1
pkgdesc='Powerful x86 virtualization for enterprise as well as home use (Oracle branded non-OSE)'
arch=('x86_64')
url='https://www.virtualbox.org/'
license=('GPL-3.0-only')
makedepends=(
    'at-spi2-core' # to satisfy pkgcheck
    'cairo' # to satisfy pkgcheck
    'gdk-pixbuf2' # to satisfy pkgcheck
    'gtk2' # to satisfy pkgcheck
    'gtk3' # to satisfy pkgcheck
    'pango' # to satisfy pkgcheck
    'python'
    'python-build'
    'python-installer'
    'python-setuptools'
    'python-wheel')
source=("http://download.virtualbox.org/virtualbox/${pkgver}/VirtualBox-${pkgver}-${_build}-Linux_amd64.run"
        "https://download.virtualbox.org/virtualbox/${pkgver}/VirtualBoxSDK-${pkgver}-${_build}.zip"
        "VBoxAuth-r${_rev}.h"::"https://www.virtualbox.org/svn/vbox/trunk/include/VBox/VBoxAuth.h?p=${_rev}"
        "VBoxAuthPAM-r${_rev}.c"::"https://www.virtualbox.org/svn/vbox/trunk/src/VBox/HostServices/auth/pam/VBoxAuthPAM.c?p=${_rev}"
        "VBoxAuthSimple-r${_rev}.cpp"::"https://www.virtualbox.org/svn/vbox/trunk/src/VBox/HostServices/auth/simple/VBoxAuthSimple.cpp?p=${_rev}"
        'dkms.conf'
        'vboxreload'
        '60-vboxdrv.rules'
        'vboxweb.service'
        'virtualbox.modprobe'
        'virtualbox.sysusers'
        'LICENSE.sdk'
        '013-Makefile.patch')
noextract=("VirtualBoxSDK-${pkgver}-${_build}.zip")
sha256sums=('df756c7b8a90015182f85772eb655abdd8af52aa1f973379a505beefcc7f4499'
            'da755498b14d9a9c5e5885ea6f3e8ca581af2a1bcb18b91895637eefa17f71b4'
            'c344b7196963a1d51f730b52836e7fcc91ace4c137995b91dc00c12205f097cd'
            'be189d96a70820aadcea24453c696275c7c7b9453ac7157b176d93a95796bdc8'
            '7ac1fff6f00a106fbc3fdb7e388f6072e8afb61f4352dfc530d8825222d202cd'
            '63f1e9eabedec2170bd0589aaa2bf5025ff8f8ec1764cc4823cbe446e9ce1388'
            '4001b5927348fe669a541e80526d4f9ea91b883805f102f7d571edbb482a9b9d'
            '9c5238183019f9ebc7d92a8582cad232f471eab9d3278786225abc1a1c7bf66e'
            'e6e875ef186578b53106d7f6af48e426cdaf1b4e86834f01696b8ef1c685787f'
            '07fe5c8b313cd7f01505eb9721357269a288ccd0c04e6467afb954038d6f46df'
            '2101ebb58233bbfadf3aa74381f22f7e7e508559d2b46387114bc2d8e308554c'
            '09335d7d1075df02d29cec13119538134efdf43ea73a93b0f89d0d7d4b6625a1'
            'a3ec0cab869e2d64914bffbf1c11a3c571808438656af654932f96e7a69114fd')

prepare() {
    local _extractdir="${pkgbase}-${pkgver}/VirtualBox-extracted"
    
    # extract files
    mkdir -p "$_extractdir"
    sh "VirtualBox-${pkgver}-${_build}-Linux_amd64.run" --noexec --nox11 --target "${pkgbase}-${pkgver}"
    bsdtar -xf "${pkgbase}-${pkgver}/VirtualBox.tar.bz2" -C "$_extractdir"
    bsdtar -xf "VirtualBoxSDK-${pkgver}-${_build}.zip" -C "${pkgbase}-${pkgver}"
    
    # dkms configuration
    install -D -m644 dkms.conf -t "${_extractdir}/src/vboxhost"
    sed -i "s/^\(PACKAGE_VERSION\)=.*/\1=${pkgver}/" "${_extractdir}/src/vboxhost/dkms.conf"
    
    # fix dkms build
    patch -d "$_extractdir" -Np1 -i "${srcdir}/013-Makefile.patch"
}

build() {
    cd "${pkgbase}-${pkgver}/sdk/installer/python/vboxapi"
    VBOX_INSTALL_PATH='/opt/VirtualBox' python -m build --wheel --no-isolation
}

package_virtualbox-bin() {
    depends=(
        'bash'
        'dbus'
        'dkms'
        'fontconfig'
        'freetype2'
        'gcc-libs'
        'glib2'
        'glibc'
        'hicolor-icon-theme'
        'libgl'
        'libx11'
        'libxcb'
        'libxkbcommon'
        'libxkbcommon-x11'
        'libxt'
        'wayland'
        'xcb-util-cursor'
        'xcb-util-image'
        'xcb-util-keysyms'
        'xcb-util-renderutil'
        'xcb-util-wm'
        'zlib')
    optdepends=(
        'at-spi2-core: for GTK2/GTK3 platformthemes plugins and GTK2 styles plugin'
        'cairo: for GTK3 platformthemes plugin'
        'gdk-pixbuf2: for GTK2/GTK3 platformthemes plugins and GTK2 styles plugin'
        'gtk2: for GTK2 platformthemes and styles plugins'
        'gtk3: for GTK3 platformthemes plugin'
        'pango: for GTK2/GTK3 platformthemes plugins and GTK2 styles plugin'
        'virtualbox-bin-guest-iso: for guest additions CD image'
        'virtualbox-bin-sdk: for the software developer kit'
        'virtualbox-ext-oracle: for Oracle extensions pack')
    provides=("virtualbox=${pkgver}" 'virtualbox-host-dkms' 'VIRTUALBOX-HOST-MODULES')
    conflicts=('virtualbox' 'virtualbox-host-dkms' 'virtualbox-host-modules-arch')
    replaces=('virtualbox_bin' 'virtualbox-sun')
    backup=('etc/vbox/vbox.cfg')
    options=('!debug' '!emptydirs' '!strip')
    
    local _installdir='opt/VirtualBox'
    
    # install bundled files
    install -d -m755 "${pkgdir}/opt"
    cp -Pr --no-preserve='ownership' "${pkgbase}-${pkgver}/VirtualBox-extracted" "${pkgdir}/${_installdir}"
    
    # mark binaries suid root, and make sure the directory is only writable by the user
    chmod 4755 "${pkgdir}/${_installdir}"/{VirtualBoxVM,VBox{Headless,Net{AdpCtl,DHCP,NAT},VolInfo}}
    chmod go-w "${pkgdir}/${_installdir}"
    
    # remove guest iso and bundled sdk files
    rm -r "${pkgdir}/${_installdir}"/{additions/VBoxGuestAdditions.iso,sdk}
    
    # module sources_pypath
    install -d -m755 "${pkgdir}/usr/src"
    mv "${pkgdir}/${_installdir}/src/vboxhost" "${pkgdir}/usr/src/vboxhost-${pkgver}_non_OSE"
    
    # module reloading shortcut (with a symlink with default helper)
    install -D -m755 vboxreload -t "${pkgdir}/usr/bin"
    ln -s vboxreload "${pkgdir}/usr/bin/rcvboxdrv"
    
    # do not enable KVM virtualization on module load
    install -D -m0644 virtualbox.modprobe "${pkgdir}/usr/lib/modprobe.d/virtualbox.conf"
    
    # udev rules
    ## we need to copy and not symlink VBoxCreateUSBNode.sh in /usr/lib/udev to avoid udevd
    ## to look /opt when /opt is not mounted. This can be done until VBoxCreateUSBNode.sh doesn't
    ## need more stuff from /opt
    install -D -m644 60-vboxdrv.rules -t "${pkgdir}/usr/lib/udev/rules.d"
    install -D -m755 "${pkgdir}/${_installdir}/VBoxCreateUSBNode.sh" -t "${pkgdir}/usr/lib/udev"
    install -D -m755 "${pkgdir}/${_installdir}/VBoxCreateUSBNode.sh" -t "${pkgdir}/usr/share/virtualbox"
    
    # configuration file
    install -D -m644 <(printf '%s\n' "INSTALL_DIR=/${_installdir}") "${pkgdir}/etc/vbox/vbox.cfg"
    
    # modules-load.d configuration
    install -D -m644 <(printf 'vboxdrv\nvboxnetadp\nvboxnetflt\n') "${pkgdir}/usr/lib/modules-load.d/${pkgname}.conf"
    
    # systemd
    install -D -m644 vboxweb.service -t "${pkgdir}/usr/lib/systemd/system"
    install -D -m644 virtualbox.sysusers "${pkgdir}/usr/lib/sysusers.d/virtualbox.conf"
    
    # symlinks
    local _dir
    local _file
    install -d -m755 "${pkgdir}/usr/share"/{applications,{doc,licenses}/"$pkgname",mime/packages,pixmaps}
    for _file in vboxwebsrv VirtualBox{,VM} VBox{Manage,SDL,VRDP,Headless,Autostart,BalloonCtrl,BugReport,DTrace}
    do
        ln -s "../../${_installdir}/VBox.sh" "${pkgdir}/usr/bin/${_file}"
        [ "$_file" != 'vboxwebsrv' ] && ln -s "../../${_installdir}/VBox.sh" "${pkgdir}/usr/bin/${_file,,}"
    done
    ln -s "../../../${_installdir}/VBoxSysInfo.sh" "${pkgdir}/usr/share/virtualbox/VBoxSysInfo.sh"
    ln -s "../../../usr/src/vboxhost-${pkgver}_non_OSE" "${pkgdir}/${_installdir}/src/vboxhost"
    ln -s "../../../${_installdir}/VBox.png" "${pkgdir}/usr/share/pixmaps/VBox.png"
    ln -s "../../../${_installdir}/virtualbox.desktop" "${pkgdir}/usr/share/applications/virtualbox.desktop"
    ln -s "../../../../${_installdir}/virtualbox.xml" "${pkgdir}/usr/share/mime/packages/virtualbox.xml"
    ln -s "../../../../${_installdir}/UserManual.pdf" "${pkgdir}/usr/share/doc/${pkgname}/UserManual.pdf"
    ln -s "../../../../${_installdir}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    ## hicolor icons
    while read -r -d '' _file
    do
        if grep -Eq '/virtualbox\.(png|svg)$' <<< "$_file"
        then
            _dir="${_file%/*}/apps"
        else
            _dir="${_file%/*}/mimetypes"
        fi
        install -d -m755 "${pkgdir}/usr/share/icons/hicolor/${_dir}"
        ln -s "../../../../../../${_installdir}/icons/${_dir%/*}/${_file##*/}" \
            "${pkgdir}/usr/share/icons/hicolor/${_dir}/${_file##*/}"
    done < <(find "${pkgdir}/${_installdir}/icons" -type f -print0 | sed -z "s|${pkgdir}/${_installdir}/icons/||")
    ## workaround for unsupported $ORIGIN/.. in VBoxC.so
    for _file in VBox{RT,XPCOM}.so
    do
        ln -s "../${_file}" "${pkgdir}/${_installdir}/components/${_file}"
    done
    
    # https://www.virtualbox.org/ticket/22193
    # https://bbs.archlinux.org/viewtopic.php?pid=2199183#p2199183
    ln -s ../../usr/lib/libdl.so.2 "${pkgdir}/${_installdir}/libdl.so"
    ln -s ../../usr/lib/libpthread.so.0 "${pkgdir}/${_installdir}/libpthread.so"
    ln -sr /usr/lib/libdl.so.2 "${srcdir}/${pkgbase}-${pkgver}/VirtualBox-extracted/libdl.so"
    ln -sr /usr/lib/libpthread.so.0 "${srcdir}/${pkgbase}-${pkgver}/VirtualBox-extracted/libpthread.so"
}

package_virtualbox-bin-guest-iso() {
    pkgdesc='VirtualBox guest additions ISO image for use with virtualbox-bin package'
    arch=('any')
    provides=('virtualbox-guest-iso')
    
    install -D -m644 "${pkgbase}-${pkgver}/VirtualBox-extracted/additions/VBoxGuestAdditions.iso" \
        -t "${pkgdir}/opt/VirtualBox/additions"
}

package_virtualbox-bin-sdk() {
    pkgdesc='VirtualBox software developer kit for use with virtualbox-bin package'
    arch=('any')
    license=('LGPL-2.1-only' 'GPL-3.0-only' 'LicenseRef-Custom')
    depends=('python')
    optdepends=('java-runtime: for webservice java bindings')
    provides=('virtualbox-sdk')
    conflicts=('virtualbox-sdk')
    
    local _dir
    local _installdir='opt/VirtualBox'
    
    install -d -m755 "${pkgdir}/${_installdir}/sdk"
    while read -r -d '' _dir
    do
        cp -Pr --no-preserve='ownership' "$_dir" "${pkgdir}/${_installdir}/sdk"
    done < <(find "${pkgbase}-${pkgver}/sdk" -mindepth 1 -maxdepth 1 -type d ! -name 'installer' -print0)
    
    install -D -m644 "VBoxAuth-r${_rev}.h"    "${pkgdir}/${_installdir}/sdk/bindings/auth/include/VBoxAuth.h"
    install -D -m644 "VBoxAuthPAM-r${_rev}.c" "${pkgdir}/${_installdir}/sdk/bindings/auth/VBoxAuthPAM.cpp"
    install -D -m644 "VBoxAuthSimple-r${_rev}.cpp" "${pkgdir}/${_installdir}/sdk/bindings/auth/VBoxAuthSimple.cpp"
    install -D -m644 LICENSE.sdk "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
    
    python -m installer --destdir="$pkgdir" "${pkgbase}-${pkgver}/sdk/installer/python/vboxapi/dist"/*.whl
    
    local _sitepkgs
    _sitepkgs="$(python -c 'import site; print(site.getsitepackages()[0])')"
    ln -s "../../../../${_installdir}/sdk/bindings/xpcom/python/xpcom" "${pkgdir}${_sitepkgs}/xpcom"
}
